# Implementing Projectiles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/implementing-projectiles-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/implementing-projectiles-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:56

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34beeb93-3a0c-44bb-8579-aea84a8662c9/fps-implementing-projectile-final-result.gif)

This is what you'll see at the end of this section.

## Goals

The purpose of this section is to show you how to implement projectiles for your First Person Shooter game.

## Objectives

By the end of this section of the tutorial, you'll be able to:

-   Add Projectiles to Your Game
-   Implement Shooting
-   Set Up Projectile Collision and Lifetime
-   Get Your Projectiles to Interact with the World
-   Add Crosshairs to Your Viewport

## Steps

-   3.1 - Adding Projectiles to Your Game
-   3.2 - Implementing Shooting
-   3.3 - Setting Up Projectile Collision and Lifetime
-   3.4 - Getting Projectiles to Interact with the World
-   3.5 - Adding Crosshairs to Your Viewport

## 3.1 - Adding Projectiles to your Game

Now that you have set up your character, it's time to implement a projectile weapon. You are going to program a simple grenade-like projectile to shoot from the center of the screen and fly until it collides with the world. During this step, you are going to add input and create a new code class for our projectile.

### Adding Fire Action Mapping

1.  Click the **Edit** in the **Main** menu panel, select **Project Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8356f201-3233-4bb2-9b85-e68d15f48cdb/01-open-project-settings.png)
2.  Under the **Engine** heading on the left side of the **Project Settings** tab, click **Input**.
    
3.  Under the **Bindings** on the right side, click the **(+)** sign next to **Action Mappings**.
    
4.  Click the **arrow** to the left of **Action Mappings**.
    
5.  Type **Fire** into the text field that appears.
    
6.  In the dropdown menu, select **Left Mouse Button** from the **Mouse** dropdown list.
    
7.  Your input settings should now look like the following:
    
    Click for full image.
    
8.  Close the **Project Settings** menu.
    

### Adding a Projectile Class

1.  Click the **Tools** in the **Main** menu panel, select **New C++ Class...**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bceb8e17-5d3c-45f5-ba52-c424dae8354e/03-new-cpp-class.png)
2.  The **Choose Parent Class** window appears. Select **Actor** as the parent class, and click **Next**.
    
    Click for full image.
    
3.  Name the new class **FPSProjectile**, then click **Create Class**.
    
    Click for full image.
    

### Adding a USphere Component

1.  The **Visual Studio** appears automatically with opened `FPSProjectile.h` header file and `FPSProjectile.cpp` implementation file, when C++ class will be created.
    
2.  Navigate to the `FPSProjectile.h` class header file.
    
3.  Add the [SphereComponent](/documentation/en-us/unreal-engine/API/Runtime/Engine/Components/USphereComponent) header file:
    
    FPSProjectile.h
    
    ```
        `#include "Components/SphereComponent.h"`
    Copy full snippet
    ```
    #include "Components/SphereComponent.h"
4.  For adding a reference to a `USphereComponent` in the `FPSProjectile` interface, add following code to the `FPSProjectile.h` under `public` access specifier:
    
    FPSProjectile.h
    
    ```
        `// Sphere collision component.     UPROPERTY(VisibleDefaultsOnly, Category = Projectile)     USphereComponent* CollisionComponent;`
    Copy full snippet
    ```
    // Sphere collision component. UPROPERTY(VisibleDefaultsOnly, Category = Projectile) USphereComponent\* CollisionComponent;
5.  `FPSProjectile.h` should now look like the following:
    
    FPSProjectile.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #pragma once      #include "CoreMinimal.h"     #include "GameFramework/Actor.h"     #include "Components/SphereComponent.h"     #include "FPSProjectile.generated.h"      UCLASS()     class FPSPROJECT_API AFPSProjectile : public AActor     {         GENERATED_BODY()      public:          // Sets default values for this actor's properties         AFPSProjectile();      protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;      public:         // Called every frame         virtual void Tick( float DeltaTime ) override;          // Sphere collision component         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         USphereComponent* CollisionComponent;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "Components/SphereComponent.h" #include "FPSProjectile.generated.h" UCLASS() class FPSPROJECT\_API AFPSProjectile : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AFPSProjectile(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Sphere collision component UPROPERTY(VisibleDefaultsOnly, Category = Projectile) USphereComponent\* CollisionComponent; };
6.  Navigate to the `FPSProjectile.cpp` class implementation file.
    
7.  Add the following code to the `AFPSProjectile` constructor (after `PrimaryActorTick.bcanEverTick`) in `FPSProjectile.cpp`:
    
    FPSProjectile.cpp
    
    ```
        `if(!RootComponent)     {         RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));     } 		     if(!CollisionComponent)     {         // Use a sphere as a simple collision representation.         CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));         // Set the sphere's collision radius.         CollisionComponent->InitSphereRadius(15.0f);         // Set the root component to be the collision component.         RootComponent = CollisionComponent;     }`
    Copy full snippet
    ```
    if(!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if(!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; }
    
    You are making `CollisionComponent` a `RootComponent` since the simulation will drive it.
    
8.  `FPSProjectile.cpp` should now look like the following:
    
    FPSProjectile.cpp
    
    ```
         `// Copyright Epic Games, Inc. All Rights Reserved.       #include "FPSProjectile.h"       // Sets default values      AFPSProjectile::AFPSProjectile()      {          // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.          PrimaryActorTick.bCanEverTick = true;           if(!RootComponent)          {              RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));          }           if(!CollisionComponent)          {              // Use a sphere as a simple collision representation.              CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));              // Set the sphere's collision radius.              CollisionComponent->InitSphereRadius(15.0f);              // Set the root component to be the collision component.              RootComponent = CollisionComponent;          }      }       // Called when the game starts or when spawned      void AFPSProjectile::BeginPlay()      {          Super::BeginPlay();       }       // Called every frame      void AFPSProjectile::Tick( float DeltaTime )      {          Super::Tick( DeltaTime );       }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if(!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if(!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); }

### Adding a Projectile Movement Component

1.  Navigate to the `FPSProjectile.h` class header file.
    
2.  Add the [ProjectileMovementComponent](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/UProjectileMovementComponent) header file.
    
    FPSProjectile.h
    
    ```
        `#include "GameFramework/ProjectileMovementComponent.h"`
    Copy full snippet
    ```
    #include "GameFramework/ProjectileMovementComponent.h"
3.  Add the following code to `FPSProjectile.h`, under `public` access specifier:
    
    FPSProjectile.h
    
    ```
        `// Projectile movement component.     UPROPERTY(VisibleAnywhere, Category = Movement)     UProjectileMovementComponent* ProjectileMovementComponent;`
    Copy full snippet
    ```
    // Projectile movement component. UPROPERTY(VisibleAnywhere, Category = Movement) UProjectileMovementComponent\* ProjectileMovementComponent;
4.  `FPSProjectile.h` should now look like the following:
    
    FPSProjectile.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #pragma once      #include "CoreMinimal.h"     #include "GameFramework/Actor.h"     #include "Components/SphereComponent.h"     #include "GameFramework/ProjectileMovementComponent.h"     #include "FPSProjectile.generated.h"      UCLASS()     class FPSPROJECT_API AFPSProjectile : public AActor     {         GENERATED_BODY()      public:          // Sets default values for this actor's properties         AFPSProjectile();      protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;      public:         // Called every frame         virtual void Tick( float DeltaTime ) override;          // Sphere collision component.         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         USphereComponent* CollisionComponent;          // Projectile movement component.         UPROPERTY(VisibleAnywhere, Category = Movement)         UProjectileMovementComponent* ProjectileMovementComponent;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "Components/SphereComponent.h" #include "GameFramework/ProjectileMovementComponent.h" #include "FPSProjectile.generated.h" UCLASS() class FPSPROJECT\_API AFPSProjectile : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AFPSProjectile(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Sphere collision component. UPROPERTY(VisibleDefaultsOnly, Category = Projectile) USphereComponent\* CollisionComponent; // Projectile movement component. UPROPERTY(VisibleAnywhere, Category = Movement) UProjectileMovementComponent\* ProjectileMovementComponent; };
5.  Navigate to the `FPSProjectile.cpp` class implementation file.
    
6.  Add the following lines of code to the `AFPSProjectile` constructor in `FPSProjectile.cpp`:
    
    FPSProjectile.cpp
    
    ```
        `if(!ProjectileMovementComponent)     {         // Use this component to drive this projectile's movement.         ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));         ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);         ProjectileMovementComponent->InitialSpeed = 3000.0f;         ProjectileMovementComponent->MaxSpeed = 3000.0f;         ProjectileMovementComponent->bRotationFollowsVelocity = true;         ProjectileMovementComponent->bShouldBounce = true;         ProjectileMovementComponent->Bounciness = 0.3f;         ProjectileMovementComponent->ProjectileGravityScale = 0.0f;     }`
    Copy full snippet
    ```
    if(!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; }
7.  `FPSProjectile.cpp` should now look like the following:
    
    FPSProjectile.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #include "FPSProjectile.h"      // Sets default values     AFPSProjectile::AFPSProjectile()     {         // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;         if(!RootComponent)         {             RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));         }          if(!CollisionComponent)         {             // Use a sphere as a simple collision representation.             CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));             // Set the sphere's collision radius.             CollisionComponent->InitSphereRadius(15.0f);             // Set the root component to be the collision component.             RootComponent = CollisionComponent;         }          if(!ProjectileMovementComponent)         {             // Use this component to drive this projectile's movement.             ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));             ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);             ProjectileMovementComponent->InitialSpeed = 3000.0f;             ProjectileMovementComponent->MaxSpeed = 3000.0f;             ProjectileMovementComponent->bRotationFollowsVelocity = true;             ProjectileMovementComponent->bShouldBounce = true;             ProjectileMovementComponent->Bounciness = 0.3f;             ProjectileMovementComponent->ProjectileGravityScale = 0.0f;         }     }      // Called when the game starts or when spawned     void AFPSProjectile::BeginPlay()     {         Super::BeginPlay();      }      // Called every frame     void AFPSProjectile::Tick( float DeltaTime )     {         Super::Tick( DeltaTime );      }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if(!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if(!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } if(!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; } } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); }

### Setting the Projectile's Initial Velocity

1.  Navigate to the `FPSProjectile.h` class header file.
    
2.  Add the following function declaration in `FPSProjectile.h`, under `public` access specifier:
    
    FPSProjectile.h
    
    ```
        `// Function that initializes the projectile's velocity in the shoot direction.     void FireInDirection(const FVector& ShootDirection);`
    Copy full snippet
    ```
    // Function that initializes the projectile's velocity in the shoot direction. void FireInDirection(const FVector& ShootDirection);
    
    This function will be responsible for launching the projectile.
    
3.  `FPSProjectile.h` should now look like the following:
    
    FPSProjectile.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #pragma once      #include "CoreMinimal.h"     #include "GameFramework/Actor.h"     #include "Components/SphereComponent.h"     #include "GameFramework/ProjectileMovementComponent.h"     #include "FPSProjectile.generated.h"      UCLASS()     class FPSPROJECT_API AFPSProjectile : public AActor     {         GENERATED_BODY()      public:          // Sets default values for this actor's properties         AFPSProjectile();      protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;      public:         // Called every frame         virtual void Tick( float DeltaTime ) override;          // Sphere collision component.         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         USphereComponent* CollisionComponent;          // Projectile movement component.         UPROPERTY(VisibleAnywhere, Category = Movement)         UProjectileMovementComponent* ProjectileMovementComponent;          // Function that initializes the projectile's velocity in the shoot direction.         void FireInDirection(const FVector& ShootDirection);     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "Components/SphereComponent.h" #include "GameFramework/ProjectileMovementComponent.h" #include "FPSProjectile.generated.h" UCLASS() class FPSPROJECT\_API AFPSProjectile : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AFPSProjectile(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Sphere collision component. UPROPERTY(VisibleDefaultsOnly, Category = Projectile) USphereComponent\* CollisionComponent; // Projectile movement component. UPROPERTY(VisibleAnywhere, Category = Movement) UProjectileMovementComponent\* ProjectileMovementComponent; // Function that initializes the projectile's velocity in the shoot direction. void FireInDirection(const FVector& ShootDirection); };
4.  Navigate to the `FPSProjectile.cpp` class implementation file.
    
5.  Add the following function definition to `FPSProjectile.cpp`:
    
    FPSProjectile.cpp
    
    ```
        `// Function that initializes the projectile's velocity in the shoot direction.     void AFPSProjectile::FireInDirection(const FVector& ShootDirection)     {         ProjectileMovementComponent->Velocity = ShootDirection * ProjectileMovementComponent->InitialSpeed;     }`
    Copy full snippet
    ```
    // Function that initializes the projectile's velocity in the shoot direction. void AFPSProjectile::FireInDirection(const FVector& ShootDirection) { ProjectileMovementComponent->Velocity = ShootDirection \* ProjectileMovementComponent->InitialSpeed; }
    
    You only needed to supply a launch direction because the projectile's speed is defined by `ProjectileMovementComponent`.
    
6.  `FPSProjectile.cpp` should now look like the following:
    
    FPSProjectile.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #include "FPSProjectile.h"      // Sets default values     AFPSProjectile::AFPSProjectile()     {         // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;          if(!RootComponent)         {             RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));         }              if (!CollisionComponent)         {             // Use a sphere as a simple collision representation.             CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));             // Set the sphere's collision radius.             CollisionComponent->InitSphereRadius(15.0f);             // Set the root component to be the collision component.             RootComponent = CollisionComponent;         }          if(!ProjectileMovementComponent)         {             // Use this component to drive this projectile's movement.             ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));             ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);             ProjectileMovementComponent->InitialSpeed = 3000.0f;             ProjectileMovementComponent->MaxSpeed = 3000.0f;             ProjectileMovementComponent->bRotationFollowsVelocity = true;             ProjectileMovementComponent->bShouldBounce = true;             ProjectileMovementComponent->Bounciness = 0.3f;             ProjectileMovementComponent->ProjectileGravityScale = 0.0f;         }     }      // Called when the game starts or when spawned     void AFPSProjectile::BeginPlay()     {         Super::BeginPlay();      }      // Called every frame     void AFPSProjectile::Tick( float DeltaTime )     {         Super::Tick( DeltaTime );      }      // Function that initializes the projectile's velocity in the shoot direction.     void AFPSProjectile::FireInDirection(const FVector& ShootDirection)     {         ProjectileMovementComponent->Velocity = ShootDirection * ProjectileMovementComponent->InitialSpeed;     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if(!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if (!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } if(!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; } } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Function that initializes the projectile's velocity in the shoot direction. void AFPSProjectile::FireInDirection(const FVector& ShootDirection) { ProjectileMovementComponent->Velocity = ShootDirection \* ProjectileMovementComponent->InitialSpeed; }

### Binding the Fire Input Action

1.  Navigate to the **Solution Explorer** in the **Visual Studio** and open the `FPSCharacter.h` class header file.
    
2.  Add the following function declaration in `FPSCharacter.h`, under `public` access specifier:
    
    FPSCharacter.h
    
    ```
        `// Function that handles firing projectiles.     UFUNCTION()     void Fire();`
    Copy full snippet
    ```
    // Function that handles firing projectiles. UFUNCTION() void Fire();
3.  `FPSCharacter.h` should now look like the following:
    
    FPSCharacter.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #pragma once      #include "CoreMinimal.h"     #include "GameFramework/Character.h"     #include "Camera/CameraComponent.h"     #include "Components/CapsuleComponent.h"     #include "FPSCharacter.generated.h"      UCLASS()     class FPSPROJECT_API AFPSCharacter : public ACharacter     {         GENERATED_BODY()      public:         // Sets default values for this character's properties         AFPSCharacter();      protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;      public:         // Called every frame         virtual void Tick( float DeltaTime ) override;          // Called to bind functionality to input         virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;          // Handles input for moving forward and backward.         UFUNCTION()         void MoveForward(float Value);          // Handles input for moving right and left.         UFUNCTION()         void MoveRight(float Value);          // Sets jump flag when key is pressed.         UFUNCTION()         void StartJump();          // Clears jump flag when key is released.         UFUNCTION()         void StopJump();          // FPS camera         UPROPERTY(VisibleAnywhere)         UCameraComponent* FPSCameraComponent;          // First-person mesh (arms), visible only to the owning player.         UPROPERTY(VisibleDefaultsOnly, Category = Mesh)         USkeletalMeshComponent* FPSMesh; 			         // Function that handles firing projectiles.         UFUNCTION()         void Fire();     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Character.h" #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h" #include "FPSCharacter.generated.h" UCLASS() class FPSPROJECT\_API AFPSCharacter : public ACharacter { GENERATED\_BODY() public: // Sets default values for this character's properties AFPSCharacter(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) override; // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value); // Sets jump flag when key is pressed. UFUNCTION() void StartJump(); // Clears jump flag when key is released. UFUNCTION() void StopJump(); // FPS camera UPROPERTY(VisibleAnywhere) UCameraComponent\* FPSCameraComponent; // First-person mesh (arms), visible only to the owning player. UPROPERTY(VisibleDefaultsOnly, Category = Mesh) USkeletalMeshComponent\* FPSMesh; // Function that handles firing projectiles. UFUNCTION() void Fire(); };
4.  Navigate to the **Solution Explorer** in the **Visual Studio** and open the `FPSCharacter.cpp` class implementation file.
    
5.  To bind the `Fire` function, add the following code to the `SetupPlayerInputComponent` function in `FPSCharacter.cpp:`
    
    FPSCharacter.cpp
    
    ```
        `PlayerInputComponent->BindAction("Fire", IE_Pressed, this, &AFPSCharacter::Fire);`
    Copy full snippet
    ```
    PlayerInputComponent->BindAction("Fire", IE\_Pressed, this, &AFPSCharacter::Fire);
6.  Add the following function definition to `FPSCharacter.cpp`:
    
    FPSCharacter.cpp
    
    ```
        `void AFPSCharacter::Fire()     {     }`
    Copy full snippet
    ```
    void AFPSCharacter::Fire() { }
7.  `FPSCharacter.cpp` should now look like the following:
    
    FPSCharacter.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #include "FPSCharacter.h"      // Sets default values     AFPSCharacter::AFPSCharacter()     {         // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;          // Create a first person camera component.         FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));         check(FPSCameraComponent != nullptr);          // Attach the camera component to our capsule component.         FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent()));          // Position the camera slightly above the eyes.         FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight));          // Enable the pawn to control camera rotation.         FPSCameraComponent->bUsePawnControlRotation = true;          // Create a first person mesh component for the owning player.         FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh"));         check(FPSMesh != nullptr);          // Only the owning player sees this mesh.         FPSMesh->SetOnlyOwnerSee(true);          // Attach the FPS mesh to the FPS camera.         FPSMesh->SetupAttachment(FPSCameraComponent);          // Disable some environmental shadowing to preserve the illusion of having a single mesh.         FPSMesh->bCastDynamicShadow = false;         FPSMesh->CastShadow = false;          // The owning player doesn't see the regular (third-person) body mesh.         GetMesh()->SetOwnerNoSee(true);     }      // Called when the game starts or when spawned     void AFPSCharacter::BeginPlay()     {         Super::BeginPlay(); 			         check(GEngine != nullptr);          // Display a debug message for five seconds.          // The -1 "Key" value argument prevents the message from being updated or refreshed.         GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));     }      // Called every frame     void AFPSCharacter::Tick( float DeltaTime )     {         Super::Tick( DeltaTime );      }      // Called to bind functionality to input     void AFPSCharacter::SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent)     {         Super::SetupPlayerInputComponent(PlayerInputComponent);          // Set up "movement" bindings.         PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);         PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);          // Set up "look" bindings.         PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput);         PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);          // Set up "action" bindings.         PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &AFPSCharacter::StartJump);         PlayerInputComponent->BindAction("Jump", IE_Released, this, &AFPSCharacter::StopJump);         PlayerInputComponent->BindAction("Fire", IE_Pressed, this, &AFPSCharacter::Fire);     }      void AFPSCharacter::MoveForward(float Value)     {         // Find out which way is "forward" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);         AddMovementInput(Direction, Value);     }      void AFPSCharacter::MoveRight(float Value)     {         // Find out which way is "right" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);         AddMovementInput(Direction, Value);     }      void AFPSCharacter::StartJump()     {         bPressedJump = true;     }      void AFPSCharacter::StopJump()     {         bPressedJump = false;     }      void AFPSCharacter::Fire()     {     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSCharacter.h" // Sets default values AFPSCharacter::AFPSCharacter() { // Set this character to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Create a first person camera component. FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); check(FPSCameraComponent != nullptr); // Attach the camera component to our capsule component. FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent())); // Position the camera slightly above the eyes. FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight)); // Enable the pawn to control camera rotation. FPSCameraComponent->bUsePawnControlRotation = true; // Create a first person mesh component for the owning player. FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh")); check(FPSMesh != nullptr); // Only the owning player sees this mesh. FPSMesh->SetOnlyOwnerSee(true); // Attach the FPS mesh to the FPS camera. FPSMesh->SetupAttachment(FPSCameraComponent); // Disable some environmental shadowing to preserve the illusion of having a single mesh. FPSMesh->bCastDynamicShadow = false; FPSMesh->CastShadow = false; // The owning player doesn't see the regular (third-person) body mesh. GetMesh()->SetOwnerNoSee(true); } // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() { Super::BeginPlay(); check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); } // Called every frame void AFPSCharacter::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight); // Set up "look" bindings. PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput); PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput); // Set up "action" bindings. PlayerInputComponent->BindAction("Jump", IE\_Pressed, this, &AFPSCharacter::StartJump); PlayerInputComponent->BindAction("Jump", IE\_Released, this, &AFPSCharacter::StopJump); PlayerInputComponent->BindAction("Fire", IE\_Pressed, this, &AFPSCharacter::Fire); } void AFPSCharacter::MoveForward(float Value) { // Find out which way is "forward" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); } void AFPSCharacter::MoveRight(float Value) { // Find out which way is "right" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y); AddMovementInput(Direction, Value); } void AFPSCharacter::StartJump() { bPressedJump = true; } void AFPSCharacter::StopJump() { bPressedJump = false; } void AFPSCharacter::Fire() { }

### Defining the Projectile's Spawn Location

1.  When spawning the `FPSProjectile` actor, there are two points to consider when implementing the `OnFire` function, namely:
    
    -   Where to spawn the projectile.
    -   The projectile class (so that `FPSCharacter` and its derived Blueprint know what projectile to spawn).
    
    You are going to use a camera-space offset vector to determine the projectile's spawn location. You will make this parameter editable so that you can set and tweak it in your `BP_FPSCharacter` Blueprint. Ultimately, you'll be able to calculate an initial location for the projectile based on this data.
    
2.  Navigate to the `FPSCharacter.h` class header file.
    
3.  Add the following code to `FPSCharacter.h`, under `public` access specifier:
    
    FPSCharacter.h
    
    ```
        `// Gun muzzle offset from the camera location.     UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Gameplay)     FVector MuzzleOffset;`
    Copy full snippet
    ```
    // Gun muzzle offset from the camera location. UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Gameplay) FVector MuzzleOffset;
    
    `EditAnywhere` enables you to change the value of the muzzle offset within the Defaults mode of the Blueprint Editor or within the Details tab for any instance of the character. The `BlueprintReadWrite` specifier enables you to get and set the value of the muzzle offset within a Blueprint.
    
4.  Add the following code to `FPSCharacter.h` under the `protected` access specifier:
    
    FPSCharacter.h
    
    ```
        `protected:          // Projectile class to spawn.         UPROPERTY(EditDefaultsOnly, Category = Projectile)         TSubclassOf<class AFPSProjectile> ProjectileClass;`
    Copy full snippet
    ```
    protected: // Projectile class to spawn. UPROPERTY(EditDefaultsOnly, Category = Projectile) TSubclassOf<class AFPSProjectile> ProjectileClass;
    
    `EditDefaultsOnly` means that you will only be able to set the projectile class as a default on the Blueprint, not on each instance of the Blueprint.
    
5.  `FPSCharacter.h` should look like the following:
    
    FPSCharacter.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #pragma once      #include "CoreMinimal.h"     #include "GameFramework/Character.h"     #include "Camera/CameraComponent.h"     #include "Components/CapsuleComponent.h"     #include "FPSCharacter.generated.h"      UCLASS()     class FPSPROJECT_API AFPSCharacter : public ACharacter     {         GENERATED_BODY()      public:         // Sets default values for this character's properties         AFPSCharacter();      protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;          // Projectile class to spawn.         UPROPERTY(EditDefaultsOnly, Category = Projectile)         TSubclassOf<class AFPSProjectile> ProjectileClass;      public:         // Called every frame         virtual void Tick( float DeltaTime ) override;          // Called to bind functionality to input         virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;          // Handles input for moving forward and backward.         UFUNCTION()         void MoveForward(float Value);          // Handles input for moving right and left.         UFUNCTION()         void MoveRight(float Value);          // Sets jump flag when key is pressed.         UFUNCTION()         void StartJump();          // Clears jump flag when key is released.         UFUNCTION()         void StopJump();          // Function that fires projectiles.         UFUNCTION()         void Fire();          // FPS camera         UPROPERTY(VisibleAnywhere)         UCameraComponent* FPSCameraComponent;          // First-person mesh (arms), visible only to the owning player.         UPROPERTY(VisibleDefaultsOnly, Category = Mesh)         USkeletalMeshComponent* FPSMesh;          // Gun muzzle offset from the camera location.         UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Gameplay)         FVector MuzzleOffset;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Character.h" #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h" #include "FPSCharacter.generated.h" UCLASS() class FPSPROJECT\_API AFPSCharacter : public ACharacter { GENERATED\_BODY() public: // Sets default values for this character's properties AFPSCharacter(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; // Projectile class to spawn. UPROPERTY(EditDefaultsOnly, Category = Projectile) TSubclassOf<class AFPSProjectile> ProjectileClass; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) override; // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value); // Sets jump flag when key is pressed. UFUNCTION() void StartJump(); // Clears jump flag when key is released. UFUNCTION() void StopJump(); // Function that fires projectiles. UFUNCTION() void Fire(); // FPS camera UPROPERTY(VisibleAnywhere) UCameraComponent\* FPSCameraComponent; // First-person mesh (arms), visible only to the owning player. UPROPERTY(VisibleDefaultsOnly, Category = Mesh) USkeletalMeshComponent\* FPSMesh; // Gun muzzle offset from the camera location. UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Gameplay) FVector MuzzleOffset; };

### Compiling and Checking Your Code

It is now time to compile and check your newly implemented projectile code.

1.  Save all of your header and implementation files in **Visual Studio**.
    
2.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
3.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6b35da3-f6b2-45a4-b4dd-edbd70af8b9f/06-build-project.png)
    
    The purpose of this step is to catch any build errors before moving onto the next step. If you encounter any build errors or warnings outside the scope of this tutorial, refer to [Coding Standard](/documentation/en-us/unreal-engine/epic-cplusplus-coding-standard-for-unreal-engine) and the [Unreal Engine API Reference](/documentation/en-us/unreal-engine/API).
    

## 3.2 - Implementing Shooting

Learn how to implement shooting for your First Person Shooter character.

### Implementing the Fire Function

1.  Navigate to the `FPSCharacter.h` class header file.
    
2.  Add the following line to `FPSCharacter.h`.
    
    FPSCharacter.h
    
    ```
        `#include "FPSProjectile.h"`
    Copy full snippet
    ```
    #include "FPSProjectile.h"
3.  Navigate to the `FPSCharacter.cpp` class implementation file.
    
4.  Add the following `Fire` function definition to `FPSCharacter.cpp`:
    
    FPSCharacter.cpp
    
    ```
        `void AFPSCharacter::Fire()     {         // Attempt to fire a projectile.         if (ProjectileClass)         {             // Get the camera transform.             FVector CameraLocation;             FRotator CameraRotation;             GetActorEyesViewPoint(CameraLocation, CameraRotation);              // Set MuzzleOffset to spawn projectiles slightly in front of the camera.             MuzzleOffset.Set(100.0f, 0.0f, 0.0f);              // Transform MuzzleOffset from camera space to world space.             FVector MuzzleLocation = CameraLocation + FTransform(CameraRotation).TransformVector(MuzzleOffset);                      // Skew the aim to be slightly upwards.             FRotator MuzzleRotation = CameraRotation;             MuzzleRotation.Pitch += 10.0f;              UWorld* World = GetWorld();             if (World)             {                 FActorSpawnParameters SpawnParams;                 SpawnParams.Owner = this;                 SpawnParams.Instigator = GetInstigator();                  // Spawn the projectile at the muzzle.                 AFPSProjectile* Projectile = World->SpawnActor<AFPSProjectile>(ProjectileClass, MuzzleLocation, MuzzleRotation, SpawnParams);                 if (Projectile)                 {                     // Set the projectile's initial trajectory.                     FVector LaunchDirection = MuzzleRotation.Vector();                     Projectile->FireInDirection(LaunchDirection);                 }             }         }     }`
    Copy full snippet
    ```
    void AFPSCharacter::Fire() { // Attempt to fire a projectile. if (ProjectileClass) { // Get the camera transform. FVector CameraLocation; FRotator CameraRotation; GetActorEyesViewPoint(CameraLocation, CameraRotation); // Set MuzzleOffset to spawn projectiles slightly in front of the camera. MuzzleOffset.Set(100.0f, 0.0f, 0.0f); // Transform MuzzleOffset from camera space to world space. FVector MuzzleLocation = CameraLocation + FTransform(CameraRotation).TransformVector(MuzzleOffset); // Skew the aim to be slightly upwards. FRotator MuzzleRotation = CameraRotation; MuzzleRotation.Pitch += 10.0f; UWorld\* World = GetWorld(); if (World) { FActorSpawnParameters SpawnParams; SpawnParams.Owner = this; SpawnParams.Instigator = GetInstigator(); // Spawn the projectile at the muzzle. AFPSProjectile\* Projectile = World->SpawnActor<AFPSProjectile>(ProjectileClass, MuzzleLocation, MuzzleRotation, SpawnParams); if (Projectile) { // Set the projectile's initial trajectory. FVector LaunchDirection = MuzzleRotation.Vector(); Projectile->FireInDirection(LaunchDirection); } } } }
5.  `FPSCharacter.h` should now look like the following:
    
    FPSCharacter.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #pragma once      #include "CoreMinimal.h"     #include "GameFramework/Character.h"     #include "Camera/CameraComponent.h"     #include "Components/CapsuleComponent.h"     #include "FPSProjectile.h"     #include "FPSCharacter.generated.h"      UCLASS()     class FPSPROJECT_API AFPSCharacter : public ACharacter     {         GENERATED_BODY()      public:         // Sets default values for this character's properties         AFPSCharacter();      protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;          // Projectile class to spawn.         UPROPERTY(EditAnywhere, Category = Projectile)         TSubclassOf<class AFPSProjectile> ProjectileClass;          public:         // Called every frame         virtual void Tick(float DeltaTime) override;              // Called to bind functionality to input        virtual void SetupPlayerInputComponent(class UIComponent* PlayerInputComponent) override;              // Handles input for moving forward and backward.         UFUNCTION()         void MoveForward(float Value);          // Handles input for moving right and left.         UFUNCTION()         void MoveRight(float Value);          // Sets jump flag when key is pressed.         UFUNCTION()         void StartJump();          // Clears jump flag when key is released.         UFUNCTION()         void StopJump();          // FPS camera         UPROPERTY(VisibleAnywhere)         UCameraComponent* FPSCameraComponent;          // First-person mesh (arms), visible only to the owning player.         UPROPERTY(VisibleDefaultsOnly, Category = Mesh)         USkeletalMeshComponent* FPSMesh; 			         // Function that fires projectiles.         UFUNCTION()         void Fire();          // Gun muzzle offset from the camera location.         UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Gameplay)         FVector MuzzleOffset;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Character.h" #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h" #include "FPSProjectile.h" #include "FPSCharacter.generated.h" UCLASS() class FPSPROJECT\_API AFPSCharacter : public ACharacter { GENERATED\_BODY() public: // Sets default values for this character's properties AFPSCharacter(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; // Projectile class to spawn. UPROPERTY(EditAnywhere, Category = Projectile) TSubclassOf<class AFPSProjectile> ProjectileClass; public: // Called every frame virtual void Tick(float DeltaTime) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UIComponent\* PlayerInputComponent) override; // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value); // Sets jump flag when key is pressed. UFUNCTION() void StartJump(); // Clears jump flag when key is released. UFUNCTION() void StopJump(); // FPS camera UPROPERTY(VisibleAnywhere) UCameraComponent\* FPSCameraComponent; // First-person mesh (arms), visible only to the owning player. UPROPERTY(VisibleDefaultsOnly, Category = Mesh) USkeletalMeshComponent\* FPSMesh; // Function that fires projectiles. UFUNCTION() void Fire(); // Gun muzzle offset from the camera location. UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Gameplay) FVector MuzzleOffset; };
6.  `FPSCharacter.cpp` should now look like the following:
    
    FPSCharacter.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #include "FPSCharacter.h"      // Sets default values     AFPSCharacter::AFPSCharacter()     {         // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;          // Create a first person camera component.         FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));         check(FPSCameraComponent != nullptr);          // Attach the camera component to our capsule component.         FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent()));          // Position the camera slightly above the eyes.         FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight));          // Enable the Pawn to control camera rotation.         FPSCameraComponent->bUsePawnControlRotation = true;          // Create a first person mesh component for the owning player.         FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh"));         check(FPSMesh != nullptr);          // Only the owning player sees this mesh.         FPSMesh->SetOnlyOwnerSee(true);          // Attach the FPS mesh to the FPS camera.         FPSMesh->SetupAttachment(FPSCameraComponent);          // Disable some environmental shadowing to preserve the illusion of having a single mesh.         FPSMesh->bCastDynamicShadow = false;         FPSMesh->CastShadow = false;          // The owning player doesn't see the regular (third-person) body mesh.         GetMesh()->SetOwnerNoSee(true);     }      // Called when the game starts or when spawned     void AFPSCharacter::BeginPlay()     {         Super::BeginPlay(); 			         check(GEngine != nullptr);          // Display a debug message for five seconds.          // The -1 "Key" value argument prevents the message from being updated or refreshed.         GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));     }      // Called every frame     void AFPSCharacter::Tick(float DeltaTime)     {         Super::Tick( DeltaTime );      }      // Called to bind functionality to input     void AFPSCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)     {         Super::SetupPlayerInputComponent(PlayerInputComponent);          // Set up "movement" bindings.         PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);         PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);          // Set up "look" bindings.         PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput);         PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);          // Set up "action" bindings.         PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &AFPSCharacter::StartJump);         PlayerInputComponent->BindAction("Jump", IE_Released, this, &AFPSCharacter::StopJump);         PlayerInputComponent->BindAction("Fire", IE_Pressed, this, &AFPSCharacter::Fire);     }      void AFPSCharacter::MoveForward(float Value)     {         // Find out which way is "forward" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);         AddMovementInput(Direction, Value);     }      void AFPSCharacter::MoveRight(float Value)     {         // Find out which way is "right" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);         AddMovementInput(Direction, Value);     }      void AFPSCharacter::StartJump()     {         bPressedJump = true;     }      void AFPSCharacter::StopJump()     {         bPressedJump = false;     }      void AFPSCharacter::Fire()     {         // Attempt to fire a projectile.         if (ProjectileClass)         {             // Get the camera transform.             FVector CameraLocation;             FRotator CameraRotation;             GetActorEyesViewPoint(CameraLocation, CameraRotation);              // Set MuzzleOffset to spawn projectiles slightly in front of the camera.             MuzzleOffset.Set(100.0f, 0.0f, 0.0f);              // Transform MuzzleOffset from camera space to world space.             FVector MuzzleLocation = CameraLocation + FTransform(CameraRotation).TransformVector(MuzzleOffset);                              // Skew the aim to be slightly upwards.             FRotator MuzzleRotation = CameraRotation;             MuzzleRotation.Pitch += 10.0f;              UWorld* World = GetWorld();             if (World)             {                 FActorSpawnParameters SpawnParams;                 SpawnParams.Owner = this;                 SpawnParams.Instigator = GetInstigator();                                      // Spawn the projectile at the muzzle.                 AFPSProjectile* Projectile = World->SpawnActor<AFPSProjectile>(ProjectileClass, MuzzleLocation, MuzzleRotation, SpawnParams);                 if (Projectile)                 {                     // Set the projectile's initial trajectory.                     FVector LaunchDirection = MuzzleRotation.Vector();                     Projectile->FireInDirection(LaunchDirection);                 }             }         }     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSCharacter.h" // Sets default values AFPSCharacter::AFPSCharacter() { // Set this character to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Create a first person camera component. FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); check(FPSCameraComponent != nullptr); // Attach the camera component to our capsule component. FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent())); // Position the camera slightly above the eyes. FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight)); // Enable the Pawn to control camera rotation. FPSCameraComponent->bUsePawnControlRotation = true; // Create a first person mesh component for the owning player. FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh")); check(FPSMesh != nullptr); // Only the owning player sees this mesh. FPSMesh->SetOnlyOwnerSee(true); // Attach the FPS mesh to the FPS camera. FPSMesh->SetupAttachment(FPSCameraComponent); // Disable some environmental shadowing to preserve the illusion of having a single mesh. FPSMesh->bCastDynamicShadow = false; FPSMesh->CastShadow = false; // The owning player doesn't see the regular (third-person) body mesh. GetMesh()->SetOwnerNoSee(true); } // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() { Super::BeginPlay(); check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); } // Called every frame void AFPSCharacter::Tick(float DeltaTime) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight); // Set up "look" bindings. PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput); PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput); // Set up "action" bindings. PlayerInputComponent->BindAction("Jump", IE\_Pressed, this, &AFPSCharacter::StartJump); PlayerInputComponent->BindAction("Jump", IE\_Released, this, &AFPSCharacter::StopJump); PlayerInputComponent->BindAction("Fire", IE\_Pressed, this, &AFPSCharacter::Fire); } void AFPSCharacter::MoveForward(float Value) { // Find out which way is "forward" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); } void AFPSCharacter::MoveRight(float Value) { // Find out which way is "right" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y); AddMovementInput(Direction, Value); } void AFPSCharacter::StartJump() { bPressedJump = true; } void AFPSCharacter::StopJump() { bPressedJump = false; } void AFPSCharacter::Fire() { // Attempt to fire a projectile. if (ProjectileClass) { // Get the camera transform. FVector CameraLocation; FRotator CameraRotation; GetActorEyesViewPoint(CameraLocation, CameraRotation); // Set MuzzleOffset to spawn projectiles slightly in front of the camera. MuzzleOffset.Set(100.0f, 0.0f, 0.0f); // Transform MuzzleOffset from camera space to world space. FVector MuzzleLocation = CameraLocation + FTransform(CameraRotation).TransformVector(MuzzleOffset); // Skew the aim to be slightly upwards. FRotator MuzzleRotation = CameraRotation; MuzzleRotation.Pitch += 10.0f; UWorld\* World = GetWorld(); if (World) { FActorSpawnParameters SpawnParams; SpawnParams.Owner = this; SpawnParams.Instigator = GetInstigator(); // Spawn the projectile at the muzzle. AFPSProjectile\* Projectile = World->SpawnActor<AFPSProjectile>(ProjectileClass, MuzzleLocation, MuzzleRotation, SpawnParams); if (Projectile) { // Set the projectile's initial trajectory. FVector LaunchDirection = MuzzleRotation.Vector(); Projectile->FireInDirection(LaunchDirection); } } } }
7.  Save `FPSCharacter.h` and `FPSCharacter.cpp` in **Visual Studio**.
    
8.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
9.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab3fdd40-67d5-4b58-b093-aa52ed1a853e/06-build-project.png)

### Importing the Projectile Mesh

Before continuing, download and extract the sample mesh from the following link:

-   [Projectile Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/46897055-4885-4e0f-87ed-8d7385a73900/sphere.zip)

1.  Open **Unreal Engine**, navigate to the **Content Browser** and open the **Content** folder.
    
2.  Right-click inside the file window of the **Content Browser** to open the **Import Asset** dialog window.
    
    Although we cover right-click import, there are three methods to import content. For information about how to import content see [Importing Assets Directly](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine):
    
3.  Click **Import to /Game...** to open the **Import** dialog window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27d2369c-be7a-4cae-b08d-5f233df5d4db/07-import.png)
4.  Locate and select the **Sphere.fbx** mesh file, where you have downloaded this file.
    
5.  Click **Open** to begin importing the mesh to your project.
    
6.  The **FBX Import Options** dialog window appears. Clicking **Import All** adds your mesh to the Project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4d6bc41-02b3-44a2-8cde-7fdd6d2928a8/08-import-option.png)
    
    Disregard the following error regarding smoothing groups:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/404c7529-cb5b-4666-8f5e-1ea7e6929750/09-message-log.png)
    
    This mesh still illustrates the first person mesh setup and it will work with the animations you'll set-up in a later section.
    
7.  Click **File** in the **Main** menu panel, select **Save all** to save your imported mesh.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6aea5c0-4377-4e9a-9b79-17fe9972e6c4/10-save-all.png)

### Adding the Projectile's Mesh

1.  Open **Visual Studio** and navigate to the **Solution Explorer**.
    
2.  In the **Solution Explorer** open the `FPSProjectile.h` class header file.
    
3.  Add the following code to `FPSProjectile.h` under the `public` access specifier:
    
    FPSProjectile.h
    
    ```
        `// Projectile mesh     UPROPERTY(VisibleDefaultsOnly, Category = Projectile)     UStaticMeshComponent* ProjectileMeshComponent;`
    Copy full snippet
    ```
    // Projectile mesh UPROPERTY(VisibleDefaultsOnly, Category = Projectile) UStaticMeshComponent\* ProjectileMeshComponent;
4.  Navigate to the **Solution Explorer** in **Visual Studio** and open the `FPSProjectile.cpp` class implementation file.
    
5.  Add the following code to the constructor in `FPSProjectile.cpp`:
    
    FPSProjectile.cpp
    
    ```
        `if(!ProjectileMeshComponent)     {         ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent"));         static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("[ADD STATIC MESH ASSET REFERENCE]"));         if(Mesh.Succeeded())         {             ProjectileMeshComponent->SetStaticMesh(Mesh.Object);         }     }`
    Copy full snippet
    ```
    if(!ProjectileMeshComponent) { ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent")); static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("\[ADD STATIC MESH ASSET REFERENCE\]")); if(Mesh.Succeeded()) { ProjectileMeshComponent->SetStaticMesh(Mesh.Object); } }
6.  Open the **Unreal Editor**. navigate to the **Content Browser**, right-click the **Sphere** static mesh and select **Copy Reference**:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa9b85f3-f2ad-4993-aea0-05d432e46e2d/11-sphere-ref.png)
7.  Open **Visual Studio**, go back to the `ProjectileMeshComponent` code in `FPSProjectile.cpp` and replace `[ADD STATIC MESH ASSET REFERENCE]` with the copied reference. Your code should look similar to the following:
    
    FPSProjectile.cpp
    
    ```
        `if(!ProjectileMeshComponent)     {         ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent"));         static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'"));         if(Mesh.Succeeded())         {             ProjectileMeshComponent->SetStaticMesh(Mesh.Object);         }     }`
    Copy full snippet
    ```
    if(!ProjectileMeshComponent) { ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent")); static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'")); if(Mesh.Succeeded()) { ProjectileMeshComponent->SetStaticMesh(Mesh.Object); } }
    
    Your asset reference path may vary depending on where you saved the Sphere mesh in the Content Browser. Also, when you paste in the copied asset reference, the reference contains the asset's type name before the asset's reference path. In your case, you will observe **StaticMesh'/Game/Sphere.Sphere'**. Make sure to remove the asset's type name (for example, StaticMesh) from the reference path.
    
8.  `FPSProjectile.h` should look like the following:
    
    FPSProjectile.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.           #pragma once           #include "CoreMinimal.h"     #include "GameFramework/Actor.h"     #include "Components/SphereComponent.h"     #include "GameFramework/ProjectileMovementComponent.h"     #include "FPSProjectile.generated.h"           UCLASS()     class FPSPROJECT_API AFPSProjectile : public AActor     {         GENERATED_BODY()              public:	         // Sets default values for this actor's properties         AFPSProjectile();           protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;           public:	         // Called every frame         virtual void Tick(float DeltaTime) override;               // Sphere collision component         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         USphereComponent* CollisionComponent;               // Projectile movement component         UPROPERTY(VisibleAnywhere, Category = Movement)         UProjectileMovementComponent* ProjectileMovementComponent;               // Function that initializes the projectile's velocity in the shoot direction.         void FireInDirection(const FVector& ShootDirection); 			         // Projectile mesh         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         UStaticMeshComponent* ProjectileMeshComponent;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "Components/SphereComponent.h" #include "GameFramework/ProjectileMovementComponent.h" #include "FPSProjectile.generated.h" UCLASS() class FPSPROJECT\_API AFPSProjectile : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AFPSProjectile(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick(float DeltaTime) override; // Sphere collision component UPROPERTY(VisibleDefaultsOnly, Category = Projectile) USphereComponent\* CollisionComponent; // Projectile movement component UPROPERTY(VisibleAnywhere, Category = Movement) UProjectileMovementComponent\* ProjectileMovementComponent; // Function that initializes the projectile's velocity in the shoot direction. void FireInDirection(const FVector& ShootDirection); // Projectile mesh UPROPERTY(VisibleDefaultsOnly, Category = Projectile) UStaticMeshComponent\* ProjectileMeshComponent; };
9.  `FPSProjectile.cpp` should look like the following:
    
    FPSProjectile.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.                        #include "FPSProjectile.h"               // Sets default values     AFPSProjectile::AFPSProjectile()     {         // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;                   if (!RootComponent)         {             RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));         }                   if (!CollisionComponent)         {             // Use a sphere as a simple collision representation.             CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));             // Set the sphere's collision radius.             CollisionComponent->InitSphereRadius(15.0f);             // Set the root component to be the collision component.             RootComponent = CollisionComponent;         }                   if (!ProjectileMovementComponent)         {             // Use this component to drive this projectile's movement.             ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));             ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);             ProjectileMovementComponent->InitialSpeed = 3000.0f;             ProjectileMovementComponent->MaxSpeed = 3000.0f;             ProjectileMovementComponent->bRotationFollowsVelocity = true;             ProjectileMovementComponent->bShouldBounce = true;             ProjectileMovementComponent->Bounciness = 0.3f;             ProjectileMovementComponent->ProjectileGravityScale = 0.0f;         }                   if (!ProjectileMeshComponent)         {             ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent"));             static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'"));             if (Mesh.Succeeded())             {                 ProjectileMeshComponent->SetStaticMesh(Mesh.Object);             }         }     }               // Called when the game starts or when spawned     void AFPSProjectile::BeginPlay()     {         Super::BeginPlay();                  }               // Called every frame     void AFPSProjectile::Tick(float DeltaTime)     {         Super::Tick(DeltaTime);               }               // Function that initializes the projectile's velocity in the shoot direction.     void AFPSProjectile::FireInDirection(const FVector& ShootDirection)     {         ProjectileMovementComponent->Velocity = ShootDirection * ProjectileMovementComponent->InitialSpeed;     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if (!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if (!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } if (!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; } if (!ProjectileMeshComponent) { ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent")); static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'")); if (Mesh.Succeeded()) { ProjectileMeshComponent->SetStaticMesh(Mesh.Object); } } } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick(float DeltaTime) { Super::Tick(DeltaTime); } // Function that initializes the projectile's velocity in the shoot direction. void AFPSProjectile::FireInDirection(const FVector& ShootDirection) { ProjectileMovementComponent->Velocity = ShootDirection \* ProjectileMovementComponent->InitialSpeed; }
10.  Save `FPSProjectile.h` and `FPSProjectile.cpp` in **Visual Studio**.
    
11.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
12.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9680ef8e-2861-4bed-916a-fbc5eebdd88f/06-build-project.png)

### Adding the Projectile's Material

1.  In **Visual Studio** navigate to the `FPSProjectile.h` and add the following code to `FPSProjectile.h` under the `public` access specifier:
    
    FPSProjectile.h
    
    ```
         `// Projectile material      UPROPERTY(VisibleDefaultsOnly, Category = Movement)      UMaterialInstanceDynamic* ProjectileMaterialInstance;`
    Copy full snippet
    ```
    // Projectile material UPROPERTY(VisibleDefaultsOnly, Category = Movement) UMaterialInstanceDynamic\* ProjectileMaterialInstance;
2.  Navigate to the `FPSProjectile.cpp` and add the following code to the bottom of the `if (!ProjectileMeshComponent)` constructor:
    
    FPSProjectile.cpp
    
    ```
        `static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("[ADD MATERIAL ASSET REFERENCE]"));     if (Material.Succeeded())     {         ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent);     }     ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance);     ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f));     ProjectileMeshComponent->SetupAttachment(RootComponent);`
    Copy full snippet
    ```
    static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("\[ADD MATERIAL ASSET REFERENCE\]")); if (Material.Succeeded()) { ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent); } ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance); ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f)); ProjectileMeshComponent->SetupAttachment(RootComponent);
3.  Open **Unreal Engine** and navigate to the **Content** folder of the **Content Browser**. Right-click in the file window of the **Content Browser** and select **Material**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86377ce5-7aaa-4b94-8827-aa7cb236a879/12-create-material.png)
4.  Name the new material **SphereMaterial**.
    
5.  Set up the new material's node graph with properties similar to the following:
    
    -   **Base Color:** drag off **Base Color** pin, in the window appears search for and select the **Constant3Vector** node, set it to **(R:1; G:0; B:0)**
    -   **Specular:** drag off **Specular** pin, in the window appears search for and select the **Constant** node, set its **Value** to **0.5**
    -   **Emissive Color:** drag off **Emissive Color**, in the window appears search for and select the **Constant** node, set its **Value** to **0.05**
    
    Click for full image.
    
    During this step, you are creating a basic Material asset. If you want to learn how to make more complex materials, read how to use and make Materials.
    
6.  After setting up the new material's node graph, click **Save**, and navigate to the **Content Browser**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c3f624c-24fa-4f12-810b-81e8e93fdaed/14-save-node-graph.png)
7.  Right-click the **Sphere** material and select **Copy Reference**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d072038a-73aa-4b9f-a010-7ca06c643f4d/15-material-ref.png)
8.  Go back to the `ProjectileMeshComponent` code in `FPSProjectile.cpp` and replace `[ADD MATERIAL ASSET REFERENCE]` with the copied reference. Your code should look similar to the following:
    
    FPSProjectile.cpp
    
    ```
        `static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'"));     if (Material.Succeeded())     {         ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent);     }     ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance);     ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f));     ProjectileMeshComponent->SetupAttachment(RootComponent);`
    Copy full snippet
    ```
    static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'")); if (Material.Succeeded()) { ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent); } ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance); ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f)); ProjectileMeshComponent->SetupAttachment(RootComponent);
    
    Your asset reference path may vary depending on where you saved the Sphere material in the Content Browser. Also, when you paste in the copied asset reference, the reference contains the asset's type name before the asset's reference path. In our case, you will observe **Material'/Game/Sphere.Sphere'**. Make sure to remove the asset's type name (for example, Material) from the reference path.
    
9.  `FPSProjectile.h` should look like the following:
    
    FPSProjectile.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.               #pragma once               #include "CoreMinimal.h"     #include "GameFramework/Actor.h"     #include "Components/SphereComponent.h"     #include "GameFramework/ProjectileMovementComponent.h"     #include "FPSProjectile.generated.h"               UCLASS()     class FPSPROJECT_API AFPSProjectile : public AActor     {         GENERATED_BODY()                  public:	         // Sets default values for this actor's properties         AFPSProjectile();               protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;               public:	         // Called every frame         virtual void Tick(float DeltaTime) override;                   // Sphere collision component         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         USphereComponent* CollisionComponent;                   // Projectile movement component         UPROPERTY(VisibleAnywhere, Category = Movement)         UProjectileMovementComponent* ProjectileMovementComponent;                   // Function that initializes the projectile's velocity in the shoot direction.         void FireInDirection(const FVector& ShootDirection); 		          // Projectile mesh         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         UStaticMeshComponent* ProjectileMeshComponent;                   // Projectile material         UPROPERTY(VisibleDefaultsOnly, Category = Movement)         UMaterialInstanceDynamic* ProjectileMaterialInstance;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "Components/SphereComponent.h" #include "GameFramework/ProjectileMovementComponent.h" #include "FPSProjectile.generated.h" UCLASS() class FPSPROJECT\_API AFPSProjectile : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AFPSProjectile(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick(float DeltaTime) override; // Sphere collision component UPROPERTY(VisibleDefaultsOnly, Category = Projectile) USphereComponent\* CollisionComponent; // Projectile movement component UPROPERTY(VisibleAnywhere, Category = Movement) UProjectileMovementComponent\* ProjectileMovementComponent; // Function that initializes the projectile's velocity in the shoot direction. void FireInDirection(const FVector& ShootDirection); // Projectile mesh UPROPERTY(VisibleDefaultsOnly, Category = Projectile) UStaticMeshComponent\* ProjectileMeshComponent; // Projectile material UPROPERTY(VisibleDefaultsOnly, Category = Movement) UMaterialInstanceDynamic\* ProjectileMaterialInstance; };
10.  `FPSProjectile.cpp` should look like the following:
    
    FPSProjectile.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.                #include "FPSProjectile.h"           // Sets default values     AFPSProjectile::AFPSProjectile()     {         // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;               if (!RootComponent)         {             RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));         }               if (!CollisionComponent)         {             // Use a sphere as a simple collision representation.             CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));             // Set the sphere's collision radius.             CollisionComponent->InitSphereRadius(15.0f);             // Set the root component to be the collision component.             RootComponent = CollisionComponent;         }               if (!ProjectileMovementComponent)         {             // Use this component to drive this projectile's movement.             ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));             ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);             ProjectileMovementComponent->InitialSpeed = 3000.0f;             ProjectileMovementComponent->MaxSpeed = 3000.0f;             ProjectileMovementComponent->bRotationFollowsVelocity = true;             ProjectileMovementComponent->bShouldBounce = true;             ProjectileMovementComponent->Bounciness = 0.3f;             ProjectileMovementComponent->ProjectileGravityScale = 0.0f;         }               if (!ProjectileMeshComponent)         {             ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent"));             static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'"));             if (Mesh.Succeeded())             {                 ProjectileMeshComponent->SetStaticMesh(Mesh.Object);             }                   static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'"));             if (Material.Succeeded())             {                 ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent);             }             ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance);             ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f));             ProjectileMeshComponent->SetupAttachment(RootComponent);         }     }           // Called when the game starts or when spawned     void AFPSProjectile::BeginPlay()     {         Super::BeginPlay();              }           // Called every frame     void AFPSProjectile::Tick(float DeltaTime)     {         Super::Tick(DeltaTime);           }           // Function that initializes the projectile's velocity in the shoot direction.     void AFPSProjectile::FireInDirection(const FVector& ShootDirection)     {         ProjectileMovementComponent->Velocity = ShootDirection * ProjectileMovementComponent->InitialSpeed;     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if (!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if (!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } if (!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; } if (!ProjectileMeshComponent) { ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent")); static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'")); if (Mesh.Succeeded()) { ProjectileMeshComponent->SetStaticMesh(Mesh.Object); } static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'")); if (Material.Succeeded()) { ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent); } ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance); ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f)); ProjectileMeshComponent->SetupAttachment(RootComponent); } } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick(float DeltaTime) { Super::Tick(DeltaTime); } // Function that initializes the projectile's velocity in the shoot direction. void AFPSProjectile::FireInDirection(const FVector& ShootDirection) { ProjectileMovementComponent->Velocity = ShootDirection \* ProjectileMovementComponent->InitialSpeed; }
11.  Open **UE**, navigate to the **Blueprints** folder in the **Content Browser** and open the **BP\_FPSCharacter** file.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1685f2f0-76ef-4708-b346-868ae8a8cdc7/16-bp-fps-character.png)
12.  Open the **Full Blueprint Editor** (if necessary), navigate to **Components** panel and select **BP\_FPSCharacter (Self)** component.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d486e90-22aa-496d-863b-9f120c0fce79/17-component-character.png)
13.  Navigate to the **Detail** panel in the opened **Blueprint Editor**.
    
14.  Find the **Projectile** section, and in the dropdown next to **Projectile Class**, select **FPSProjectile**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed2aa82a-e367-48a1-8e89-8e6a90ae0eb0/18-set-projectile-class.png)
    
    If you can't find the **FPSProjectile** in the opened dropdown menu, please rerun **Unreal Engine**.
    
15.  Click **Compile** and **Save** buttons.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3120862-41fe-4dfb-8e94-4f840013f4d9/19-compile-save.png)
16.  Open the **Visual Studio**, navigate to the **Solution Explorer** and select **FPSProject**.
    
17.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd7ad464-c6b6-451e-a031-ebcbe6d3f61a/06-build-project.png)
18.  Run the game in PIE mode to verify that the Static Mesh and Material are being spawned in the scene.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03ed2863-1f36-47b3-8ccc-ef1cb8835a65/fps-implementing-projectile-animation-1.gif)
    
    While firing the projectiles, you will observe in the **Outliner** that the number of projectiles keeps increasing because they have no defined lifespan.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bfa5f66-1958-47f5-be63-cd563d779176/20-increasing.png)
    
    In the next section, tutorial shows you how to define the projectile's initial lifespan.
    

## 3.3 - Setting up Projectile Collision and Lifetime

Currently, our projectiles:

-   Live forever (they never disappear from the Scene Outliner)
-   Don't collide with other objects in the world

During this step, you are going to set up projectile collision and lifetime.

### Limiting the Projectile's Life Span

1.  Open the **Visual Studio** and navigate to the **Solution Explorer**.
    
2.  In the **Solution Explorer** open the `FPSProjectile.cpp` class implementation file.
    
3.  Add the following code to the `AFPSProjectile::AFPSProjectile()` constructor of the `FPSProjectile.cpp` to set the projectile's lifespan:
    
    FPSProjectile.cpp
    
    ```
        `// Delete the projectile after 3 seconds.     InitialLifeSpan = 3.0f;`
    Copy full snippet
    ```
    // Delete the projectile after 3 seconds. InitialLifeSpan = 3.0f;
4.  `FPSProjectile.cpp` should look like the following:
    
    FPSProjectile.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.                        #include "FPSProjectile.h"               // Sets default values     AFPSProjectile::AFPSProjectile()     {         // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;                   if (!RootComponent)         {             RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));         }                   if (!CollisionComponent)         {             // Use a sphere as a simple collision representation.             CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));             // Set the sphere's collision radius.             CollisionComponent->InitSphereRadius(15.0f);             // Set the root component to be the collision component.             RootComponent = CollisionComponent;         }                   if (!ProjectileMovementComponent)         {             // Use this component to drive this projectile's movement.             ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));             ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);             ProjectileMovementComponent->InitialSpeed = 3000.0f;             ProjectileMovementComponent->MaxSpeed = 3000.0f;             ProjectileMovementComponent->bRotationFollowsVelocity = true;             ProjectileMovementComponent->bShouldBounce = true;             ProjectileMovementComponent->Bounciness = 0.3f;             ProjectileMovementComponent->ProjectileGravityScale = 0.0f;         }                   if (!ProjectileMeshComponent)         {             ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent"));             static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'"));             if (Mesh.Succeeded())             {                 ProjectileMeshComponent->SetStaticMesh(Mesh.Object);             }                       static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'"));             if (Material.Succeeded())             {                 ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent);             }             ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance);             ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f));             ProjectileMeshComponent->SetupAttachment(RootComponent);         }                   // Delete the projectile after 3 seconds.         InitialLifeSpan = 3.0f;     }               // Called when the game starts or when spawned     void AFPSProjectile::BeginPlay()     {         Super::BeginPlay();                  }               // Called every frame     void AFPSProjectile::Tick(float DeltaTime)     {         Super::Tick(DeltaTime);               }               // Function that initializes the projectile's velocity in the shoot direction.     void AFPSProjectile::FireInDirection(const FVector& ShootDirection)     {         ProjectileMovementComponent->Velocity = ShootDirection * ProjectileMovementComponent->InitialSpeed;     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if (!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if (!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } if (!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; } if (!ProjectileMeshComponent) { ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent")); static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'")); if (Mesh.Succeeded()) { ProjectileMeshComponent->SetStaticMesh(Mesh.Object); } static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'")); if (Material.Succeeded()) { ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent); } ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance); ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f)); ProjectileMeshComponent->SetupAttachment(RootComponent); } // Delete the projectile after 3 seconds. InitialLifeSpan = 3.0f; } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick(float DeltaTime) { Super::Tick(DeltaTime); } // Function that initializes the projectile's velocity in the shoot direction. void AFPSProjectile::FireInDirection(const FVector& ShootDirection) { ProjectileMovementComponent->Velocity = ShootDirection \* ProjectileMovementComponent->InitialSpeed; }
5.  Save your file.
    
6.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
7.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7abad6d-6f9d-4db3-be10-ce4bd8b7ec9d/06-build-project.png)
8.  To verify that the projectiles are being destroyed after three seconds, run the game in PIE mode.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3268500-43a6-4f7e-a3a2-ad75e134909e/fps-implementing-projectile-animation-2.gif)
    
    As verified in the Outliner, every spawned projectile will disappear from the scene after three seconds.
    

### Editing the Projectile's Collision Settings

Unreal Engine comes packaged with several preset collision channels; however, the Engine also provides customizable channels that game projects can use.

1.  To create a custom collision channel, navigate to **Unreal Engine** and open **Project Settings**, select the **Engine** heading on the left side and select **Collision**, expand **Preset** section on the right side.
    
    Click for full image.
    
2.  Navigate to the **Object Channels** and select **New Object Channel...** to create a new collision channel. Name your new collision channel **Projectile** and verify that the **Default Response** is set to **Block** before clicking **Accept**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6398235b-a6ce-4526-8146-b622a0ef3580/22-new-object-channel.png)
3.  Select **New...** under **Preset** and name your new profile **Projectile**. Reference the following image to set your collision presets and click **Accept**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66ba1dea-759e-4365-8c6c-391c4d19011f/23-new-preset-profile.png)

This collision profile specifies that the projectile will be blocked by Static Actors, Dynamic Actors, Actors simulating Physics, Vehicles, and Destructible Actors. Also, this collision profile specifies that the projectile overlaps Pawns.

### Using the New Collision Channel's Settings

1.  Open the **Visual Studio** and navigate to the `FPSProjectile.cpp` class implementation file.
    
2.  In the `FPSProjectile` constructor, add the following line to the `if (!CollisionComponent)` block, after `CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));`:
    
    FPSProjectile.cpp
    
    ```
        `// Set the sphere's collision profile name to "Projectile".     CollisionComponent->BodyInstance.SetCollisionProfileName(TEXT("Projectile"));`
    Copy full snippet
    ```
    // Set the sphere's collision profile name to "Projectile". CollisionComponent->BodyInstance.SetCollisionProfileName(TEXT("Projectile"));
3.  `FPSProjectile.cpp` should now look like the following:
    
    FPSProjectile.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #include "FPSProjectile.h"      // Sets default values     AFPSProjectile::AFPSProjectile()     {         // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;          if (!RootComponent)         {             RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));         }          if (!CollisionComponent)         {             // Use a sphere as a simple collision representation.             CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));             // Set the sphere's collision profile name to "Projectile".             CollisionComponent->BodyInstance.SetCollisionProfileName(TEXT("Projectile"));             // Set the sphere's collision radius.             CollisionComponent->InitSphereRadius(15.0f);             // Set the root component to be the collision component.             RootComponent = CollisionComponent;         }          if (!ProjectileMovementComponent)         {             // Use this component to drive this projectile's movement.             ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));             ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);             ProjectileMovementComponent->InitialSpeed = 3000.0f;             ProjectileMovementComponent->MaxSpeed = 3000.0f;             ProjectileMovementComponent->bRotationFollowsVelocity = true;             ProjectileMovementComponent->bShouldBounce = true;             ProjectileMovementComponent->Bounciness = 0.3f;             ProjectileMovementComponent->ProjectileGravityScale = 0.0f;         }          if (!ProjectileMeshComponent)         {             ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent"));             static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'"));             if (Mesh.Succeeded())             {                 ProjectileMeshComponent->SetStaticMesh(Mesh.Object);             }              static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'"));             if (Material.Succeeded())             {                 ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent);             }             ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance);             ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f));             ProjectileMeshComponent->SetupAttachment(RootComponent);         }         // Delete the projectile after 3 seconds.         InitialLifeSpan = 3.0f;     }      // Called when the game starts or when spawned     void AFPSProjectile::BeginPlay()     {         Super::BeginPlay();              }      // Called every frame     void AFPSProjectile::Tick(float DeltaTime)     {         Super::Tick(DeltaTime);      }      // Function that initializes the projectile's velocity in the shoot direction.     void AFPSProjectile::FireInDirection(const FVector& ShootDirection)     {         ProjectileMovementComponent->Velocity = ShootDirection * ProjectileMovementComponent->InitialSpeed;     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if (!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if (!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision profile name to "Projectile". CollisionComponent->BodyInstance.SetCollisionProfileName(TEXT("Projectile")); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } if (!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; } if (!ProjectileMeshComponent) { ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent")); static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'")); if (Mesh.Succeeded()) { ProjectileMeshComponent->SetStaticMesh(Mesh.Object); } static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'")); if (Material.Succeeded()) { ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent); } ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance); ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f)); ProjectileMeshComponent->SetupAttachment(RootComponent); } // Delete the projectile after 3 seconds. InitialLifeSpan = 3.0f; } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick(float DeltaTime) { Super::Tick(DeltaTime); } // Function that initializes the projectile's velocity in the shoot direction. void AFPSProjectile::FireInDirection(const FVector& ShootDirection) { ProjectileMovementComponent->Velocity = ShootDirection \* ProjectileMovementComponent->InitialSpeed; }
4.  Save your file.
    
5.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
6.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/176bc3f6-e137-475c-8ff1-a963a44aba88/06-build-project.png)

## 3.4 - Getting Projectiles to Interact with the World

Now that you can detect the projectile's collision interactions, you can determine how to respond to those collisions. During this step, you will add an `OnHit` function to `FPSProjectile` that'll respond to collision events.

### Getting Projectiles to React to Collisions

1.  Open `FPSProjectile.h.`
    
2.  Add the following code to `FPSProjectile.h` under the `public` access specifier:
    
    FPSProjectile.h
    
    ```
        `// Function that is called when the projectile hits something.     UFUNCTION()     void OnHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComponent, FVector NormalImpulse, const FHitResult& Hit);`
    Copy full snippet
    ```
    // Function that is called when the projectile hits something. UFUNCTION() void OnHit(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComponent, FVector NormalImpulse, const FHitResult& Hit);
3.  `FPSProjectile.h` should now look like the following:
    
    FPSProjectile.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.           #pragma once           #include "CoreMinimal.h"     #include "GameFramework/Actor.h"     #include "Components/SphereComponent.h"     #include "GameFramework/ProjectileMovementComponent.h"     #include "FPSProjectile.generated.h"           UCLASS()     class FPSPROJECT_API AFPSProjectile : public AActor     {         GENERATED_BODY()              public:	         // Sets default values for this actor's properties         AFPSProjectile();           protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;           public:	         // Called every frame         virtual void Tick(float DeltaTime) override;               // Sphere collision component         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         USphereComponent* CollisionComponent;               // Projectile movement component         UPROPERTY(VisibleAnywhere, Category = Movement)         UProjectileMovementComponent* ProjectileMovementComponent; 			         // Function that initializes the projectile's velocity in the shoot direction.         void FireInDirection(const FVector& ShootDirection); 		          // Projectile mesh         UPROPERTY(VisibleDefaultsOnly, Category = Projectile)         UStaticMeshComponent* ProjectileMeshComponent; 		          // Projectile material         UPROPERTY(VisibleDefaultsOnly, Category = Movement)         UMaterialInstanceDynamic* ProjectileMaterialInstance; 		          // Function that is called when the projectile hits something.         UFUNCTION()         void OnHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComponent, FVector NormalImpulse, const FHitResult& Hit);     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "Components/SphereComponent.h" #include "GameFramework/ProjectileMovementComponent.h" #include "FPSProjectile.generated.h" UCLASS() class FPSPROJECT\_API AFPSProjectile : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AFPSProjectile(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick(float DeltaTime) override; // Sphere collision component UPROPERTY(VisibleDefaultsOnly, Category = Projectile) USphereComponent\* CollisionComponent; // Projectile movement component UPROPERTY(VisibleAnywhere, Category = Movement) UProjectileMovementComponent\* ProjectileMovementComponent; // Function that initializes the projectile's velocity in the shoot direction. void FireInDirection(const FVector& ShootDirection); // Projectile mesh UPROPERTY(VisibleDefaultsOnly, Category = Projectile) UStaticMeshComponent\* ProjectileMeshComponent; // Projectile material UPROPERTY(VisibleDefaultsOnly, Category = Movement) UMaterialInstanceDynamic\* ProjectileMaterialInstance; // Function that is called when the projectile hits something. UFUNCTION() void OnHit(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComponent, FVector NormalImpulse, const FHitResult& Hit); };
4.  Open `FPSProjectile.cpp` to add the following code:
    
    FPSProjectile.cpp
    
    ```
        `// Function that is called when the projectile hits something.     void AFPSProjectile::OnHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComponent, FVector NormalImpulse, const FHitResult& Hit)     {         if (OtherActor != this && OtherComponent->IsSimulatingPhysics())         {             OtherComponent->AddImpulseAtLocation(ProjectileMovementComponent->Velocity * 100.0f, Hit.ImpactPoint);         }         Destroy();     }`
    Copy full snippet
    ```
    // Function that is called when the projectile hits something. void AFPSProjectile::OnHit(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComponent, FVector NormalImpulse, const FHitResult& Hit) { if (OtherActor != this && OtherComponent->IsSimulatingPhysics()) { OtherComponent->AddImpulseAtLocation(ProjectileMovementComponent->Velocity \* 100.0f, Hit.ImpactPoint); } Destroy(); }
5.  In the `FPSProjectile` constructor, add the following line to the `if (!CollisionComponent)` block, after `BodyInstance.SetCollisionProfileName:`
    
    FPSProjectile.cpp
    
    ```
        `// Event called when component hits something.     CollisionComponent->OnComponentHit.AddDynamic(this, &AFPSProjectile::OnHit);`
    Copy full snippet
    ```
    // Event called when component hits something. CollisionComponent->OnComponentHit.AddDynamic(this, &AFPSProjectile::OnHit);
6.  `FPSProjectile.cpp` should now look like the following:
    
    FPSProjectile.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.      #include "FPSProjectile.h"      // Sets default values     AFPSProjectile::AFPSProjectile()     {         // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;          if (!RootComponent)         {             RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));         }          if (!CollisionComponent)         {             // Use a sphere as a simple collision representation.             CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));             // Set the sphere's collision profile name to "Projectile".             CollisionComponent->BodyInstance.SetCollisionProfileName(TEXT("Projectile"));             // Event called when component hits something.             CollisionComponent->OnComponentHit.AddDynamic(this, &AFPSProjectile::OnHit);             // Set the sphere's collision radius.             CollisionComponent->InitSphereRadius(15.0f);             // Set the root component to be the collision component.             RootComponent = CollisionComponent;         }          if (!ProjectileMovementComponent)         {             // Use this component to drive this projectile's movement.             ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));             ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);             ProjectileMovementComponent->InitialSpeed = 3000.0f;             ProjectileMovementComponent->MaxSpeed = 3000.0f;             ProjectileMovementComponent->bRotationFollowsVelocity = true;             ProjectileMovementComponent->bShouldBounce = true;             ProjectileMovementComponent->Bounciness = 0.3f;             ProjectileMovementComponent->ProjectileGravityScale = 0.0f;         }          if (!ProjectileMeshComponent)         {             ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent"));             static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'"));             if (Mesh.Succeeded())             {                 ProjectileMeshComponent->SetStaticMesh(Mesh.Object);             }              static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'"));             if (Material.Succeeded())             {                 ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent);             }             ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance);             ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f));             ProjectileMeshComponent->SetupAttachment(RootComponent);         }         // Delete the projectile after 3 seconds.         InitialLifeSpan = 3.0f;     }      // Called when the game starts or when spawned     void AFPSProjectile::BeginPlay()     {         Super::BeginPlay(); 			     }      // Called every frame     void AFPSProjectile::Tick(float DeltaTime)     {         Super::Tick(DeltaTime);      } 		     // Function that initializes the projectile's velocity in the shoot direction.     void AFPSProjectile::FireInDirection(const FVector& ShootDirection)     {         ProjectileMovementComponent->Velocity = ShootDirection * ProjectileMovementComponent->InitialSpeed;     } 		     // Function that is called when the projectile hits something.     void AFPSProjectile::OnHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComponent, FVector NormalImpulse, const FHitResult& Hit)     {         if (OtherActor != this && OtherComponent->IsSimulatingPhysics())         {             OtherComponent->AddImpulseAtLocation(ProjectileMovementComponent->Velocity * 100.0f, Hit.ImpactPoint);         }         Destroy();     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if (!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if (!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision profile name to "Projectile". CollisionComponent->BodyInstance.SetCollisionProfileName(TEXT("Projectile")); // Event called when component hits something. CollisionComponent->OnComponentHit.AddDynamic(this, &AFPSProjectile::OnHit); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } if (!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; } if (!ProjectileMeshComponent) { ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent")); static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'")); if (Mesh.Succeeded()) { ProjectileMeshComponent->SetStaticMesh(Mesh.Object); } static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'")); if (Material.Succeeded()) { ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent); } ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance); ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f)); ProjectileMeshComponent->SetupAttachment(RootComponent); } // Delete the projectile after 3 seconds. InitialLifeSpan = 3.0f; } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick(float DeltaTime) { Super::Tick(DeltaTime); } // Function that initializes the projectile's velocity in the shoot direction. void AFPSProjectile::FireInDirection(const FVector& ShootDirection) { ProjectileMovementComponent->Velocity = ShootDirection \* ProjectileMovementComponent->InitialSpeed; } // Function that is called when the projectile hits something. void AFPSProjectile::OnHit(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComponent, FVector NormalImpulse, const FHitResult& Hit) { if (OtherActor != this && OtherComponent->IsSimulatingPhysics()) { OtherComponent->AddImpulseAtLocation(ProjectileMovementComponent->Velocity \* 100.0f, Hit.ImpactPoint); } Destroy(); }

### Testing Projectile Collision

1.  Save your files in **Visual Studio**.
    
2.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
3.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5b19e27-c284-4252-8dc6-fe4b4d9ec136/06-build-project.png)
4.  After the build finishes, go back to your **FPSProject** in the **Unreal Editor**.
    
5.  Navigate to the **Outliner** and select the **Floor** Static Mesh.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12ad9ea8-c5be-4f45-b1a9-e645d5cae512/24-outliner.png)
6.  Copy and paste selected **Floor** mesh.
    
7.  Making sure that the ratio lock is unlocked (the lock icon next to the Scale row), set options of the **Transform** section in the **Detail** panel of the **Floor2** as following:
    
    -   **Location**: (0.0, 0.0, 150);
    -   **Rotation**: (0.0, 0.0, 0.0);
    -   **Scale**: (0.2, 0.2, 3.0).
8.  Scroll down to the **Physics** section and check the **Simulate Physics** box.
    
    Click on the image to zoom in.
    
9.  Click the **File** in the **Main** menu panel and select **Save All** to save your imported mesh.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42b6ceb8-f78b-41d8-a032-50037da48bb2/10-save-all.png)
10.  Click the **Play** button in the **Level Editor Toolbar**.
    
11.  To verify that projectiles are colliding with the cube, left-click your mouse button to fire projectiles and move the cube around your level.
    
    \[![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbf0c1dd-23f4-4c72-a5ae-799da3a6a51c/fps-implementing-projectile-animation-3.gif)
    
    Congratulations, your projectiles are complete!
    
12.  Press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

## 3.5 - Adding Crosshairs to your Viewport

During this step, you will add a crosshair HUD element to our game so that you can aim our projectiles.

### Importing a Crosshair Asset

Before getting started, download and extract the sample image from the following link:

-   [Sample Crosshair Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/2bf87424-078f-49cf-94df-149b14188210/crosshair_fps_tutorial.zip)

1.  Navigate to the **Content Browser** and open the **Content** folder.
    
2.  Right-click inside the file window of the **Content Browser** to open the **Import Asset** dialog window.
    
3.  Click **'Import to / Game...'** to open the **Import** dialog window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9557b043-f282-4c4f-a4b6-9660fff88801/07-import.png)
4.  Locate and select the **crosshair.TGA** image file, where you have downloaded this file.
    
5.  Click **Open** to begin importing the image file to your project.
    
6.  Click the **File** in the **Main** menu panel to save your imported mesh.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/102b1027-96e8-4ef1-a8c1-8fd381db9670/10-save-all.png)

### Adding a New HUD Class

1.  Click the **Tools** in the **Main** menu panel, **New C++ Class...** to choose your new parent class.
    
2.  The **Choose Parent Class** menu appears. Select **HUD** as the parent class and click **Next**.
    
    Click for full image.
    
3.  Name the new class **FPSHUD**, then click **Create Class**.
    
    Click for full image.
    
4.  The **Visual Studio** appears automatically with opened `FPSHUD.h` header file and `FPSHUD.cpp` implementation file, when C++ class will be created.
    
5.  Navigate to the `FPSHUD.h` class header file, and add the following variable under the `protected` access specifier:
    
    FPSHUD.h
    
    ```
        `protected: 		         // This will be drawn at the center of the screen.         UPROPERTY(EditDefaultsOnly)         UTexture2D* CrosshairTexture;`
    Copy full snippet
    ```
    protected: // This will be drawn at the center of the screen. UPROPERTY(EditDefaultsOnly) UTexture2D\* CrosshairTexture;
6.  Add the following function declaration in `FPSHUD.h` under the `public` access specifier:
    
    FPSHUD.h
    
    ```
        `public: 		         // Primary draw call for the HUD.         virtual void DrawHUD() override;`
    Copy full snippet
    ```
    public: // Primary draw call for the HUD. virtual void DrawHUD() override;
7.  Add the following header file to `FPSHUD.h`:
    
    FPSHUD.h
    
    ```
        `#include "Engine/Canvas.h"` 
    Copy full snippet
    ```
    #include "Engine/Canvas.h"
8.  `FPSHUD.h` should now look like the following:
    
    FPSHUD.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.               #pragma once               #include "CoreMinimal.h"     #include "GameFramework/HUD.h"     #include "Engine/Canvas.h"     #include "FPSHUD.generated.h"               /**      *       */     UCLASS()     class FPSPROJECT_API AFPSHUD : public AHUD     {         GENERATED_BODY()              protected:         // This will be drawn at the center of the screen.         UPROPERTY(EditDefaultsOnly)         UTexture2D* CrosshairTexture; 		     public:         // Primary draw call for the HUD.         virtual void DrawHUD() override;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/HUD.h" #include "Engine/Canvas.h" #include "FPSHUD.generated.h" /\*\* \* \*/ UCLASS() class FPSPROJECT\_API AFPSHUD : public AHUD { GENERATED\_BODY() protected: // This will be drawn at the center of the screen. UPROPERTY(EditDefaultsOnly) UTexture2D\* CrosshairTexture; public: // Primary draw call for the HUD. virtual void DrawHUD() override; };
9.  Open the `FPSHUD.cpp` implementation file and add the `DrawHUD` function:
    
    FPSHUD.cpp
    
    ```
        `void AFPSHUD::DrawHUD()     {         Super::DrawHUD();          if (CrosshairTexture)         {             // Find the center of our canvas.             FVector2D Center(Canvas->ClipX * 0.5f, Canvas->ClipY * 0.5f);              // Offset by half of the texture's dimensions so that the center of the texture aligns with the center of the Canvas.             FVector2D CrossHairDrawPosition(Center.X - (CrosshairTexture->GetSurfaceWidth() * 0.5f), Center.Y - (CrosshairTexture->GetSurfaceHeight() * 0.5f));              // Draw the crosshair at the centerpoint.             FCanvasTileItem TileItem(CrossHairDrawPosition, CrosshairTexture->Resource, FLinearColor::White);             TileItem.BlendMode = SE_BLEND_Translucent;             Canvas->DrawItem(TileItem);         }     }`
    Copy full snippet
    ```
    void AFPSHUD::DrawHUD() { Super::DrawHUD(); if (CrosshairTexture) { // Find the center of our canvas. FVector2D Center(Canvas->ClipX \* 0.5f, Canvas->ClipY \* 0.5f); // Offset by half of the texture's dimensions so that the center of the texture aligns with the center of the Canvas. FVector2D CrossHairDrawPosition(Center.X - (CrosshairTexture->GetSurfaceWidth() \* 0.5f), Center.Y - (CrosshairTexture->GetSurfaceHeight() \* 0.5f)); // Draw the crosshair at the centerpoint. FCanvasTileItem TileItem(CrossHairDrawPosition, CrosshairTexture->Resource, FLinearColor::White); TileItem.BlendMode = SE\_BLEND\_Translucent; Canvas->DrawItem(TileItem); } }
10.  Save `FPSHUD.h` and `FPSHUD.cpp` in **Visual Studio**.
    
11.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
12.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9c3ba0a-1489-4cb7-a743-213335f00336/06-build-project.png)

### Extending your CPP HUD Class to Blueprints

Now is a good time to extend the CPP HUD class to Blueprints. If you need a refresher, go to our [C++ and Blueprints](/documentation/en-us/unreal-engine/cpp-and-blueprints-example) reference page to learn more about extending C++ classes to Blueprints.

1.  Right-click the `FPSHUD` class to open the **C++ Class Actions** menu.
    
2.  Click **Create Blueprint class based on FPSHUD** to open the **Add Blueprint Class** dialog menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94195379-329a-41a8-a1ed-695803a235e4/28-create-based-bp.png)
3.  Name your new Blueprint Class **BP\_FPSHUD** and choose the Blueprints folder before clicking the **Create Blueprint Class** button.
    
    Click for full image.
    
4.  By now, you should have a newly created **BP\_FPSHUD** Blueprint Class located inside of the Blueprints folder.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b3405dc-9106-47ba-aa0d-948de3e62ac6/30-location-fpshud.png)
5.  Make sure to save your **BP\_FPSHUD** Blueprint before closing the **Blueprint Editor**.
    

### Setting the Default HUD Class

1.  Click the **Edit** in the **Main** menu panel, select **Project Settings**.
    
2.  Under the **Project** heading on the left side of the **Project Settings** tab, click on **Maps & Modes**.
    
3.  Select **BP\_FPSHUD** in the **Default HUD** dropdown menu.
    
    Click for full image.
    
4.  Close the **Project Settings** menu.
    
5.  Go back and open the **BP\_FPSHUD** in the **Blueprint Editor**.
    
6.  Now, click on the dropdown menu located in the **FPSHUD** section of the **Blueprint Editor** to select your crosshair texture.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dff28dc5-98f1-45de-88e5-f9aee36dc5e5/32-select-crosshair.png)
7.  Finally, **Compile** and **Save** the **BP\_FPSHUD** Blueprint before closing the **Blueprint Editor**.
    

### Verifying your HUD

1.  Click the **Play** button in the **Level Editor Toolbar**. You should now be able to aim the projectiles with your newly added crosshair.
    
    ![](FPS-implementing-projectile-final-result.gif)(convert:false)
    
2.  Press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

### Finished Section Code

FPSProjectile.h

```
        `// Copyright Epic Games, Inc. All Rights Reserved.                   #pragma once                   #include "CoreMinimal.h"         #include "GameFramework/Actor.h"         #include "Components/SphereComponent.h"         #include "GameFramework/ProjectileMovementComponent.h"         #include "FPSProjectile.generated.h"                   UCLASS()         class FPSPROJECT_API AFPSProjectile : public AActor         {             GENERATED_BODY()                      public:	             // Sets default values for this actor's properties             AFPSProjectile();                   protected:             // Called when the game starts or when spawned             virtual void BeginPlay() override;                   public:	             // Called every frame             virtual void Tick(float DeltaTime) override;                       // Sphere collision component             UPROPERTY(VisibleDefaultsOnly, Category = Projectile)             USphereComponent* CollisionComponent;                       // Projectile movement component             UPROPERTY(VisibleAnywhere, Category = Movement)             UProjectileMovementComponent* ProjectileMovementComponent;              			// Function that initializes the projectile's velocity in the shoot direction.             void FireInDirection(const FVector& ShootDirection);              			// Projectile mesh             UPROPERTY(VisibleDefaultsOnly, Category = Projectile)             UStaticMeshComponent* ProjectileMeshComponent;                       // Projectile material             UPROPERTY(VisibleDefaultsOnly, Category = Movement)             UMaterialInstanceDynamic* ProjectileMaterialInstance; 			 			// Function that is called when the projectile hits something.             UFUNCTION()             void OnHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComponent, FVector NormalImpulse, const FHitResult& Hit);         };`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "Components/SphereComponent.h" #include "GameFramework/ProjectileMovementComponent.h" #include "FPSProjectile.generated.h" UCLASS() class FPSPROJECT\_API AFPSProjectile : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AFPSProjectile(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick(float DeltaTime) override; // Sphere collision component UPROPERTY(VisibleDefaultsOnly, Category = Projectile) USphereComponent\* CollisionComponent; // Projectile movement component UPROPERTY(VisibleAnywhere, Category = Movement) UProjectileMovementComponent\* ProjectileMovementComponent; // Function that initializes the projectile's velocity in the shoot direction. void FireInDirection(const FVector& ShootDirection); // Projectile mesh UPROPERTY(VisibleDefaultsOnly, Category = Projectile) UStaticMeshComponent\* ProjectileMeshComponent; // Projectile material UPROPERTY(VisibleDefaultsOnly, Category = Movement) UMaterialInstanceDynamic\* ProjectileMaterialInstance; // Function that is called when the projectile hits something. UFUNCTION() void OnHit(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComponent, FVector NormalImpulse, const FHitResult& Hit); };

FPSProjectile.cpp

```
        `// Copyright Epic Games, Inc. All Rights Reserved.                            #include "FPSProjectile.h"                   // Sets default values         AFPSProjectile::AFPSProjectile()         {             // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.             PrimaryActorTick.bCanEverTick = true;                       if (!RootComponent)             {                 RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent"));             }                       if (!CollisionComponent)             {                 // Use a sphere as a simple collision representation.                 CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent"));                 // Set the sphere's collision profile name to "Projectile".                 CollisionComponent->BodyInstance.SetCollisionProfileName(TEXT("Projectile"));                 // Event called when component hits something.                 CollisionComponent->OnComponentHit.AddDynamic(this, &AFPSProjectile::OnHit);                 // Set the sphere's collision radius.                 CollisionComponent->InitSphereRadius(15.0f);                 // Set the root component to be the collision component.                 RootComponent = CollisionComponent;             }                       if (!ProjectileMovementComponent)             {                 // Use this component to drive this projectile's movement.                 ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent"));                 ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent);                 ProjectileMovementComponent->InitialSpeed = 3000.0f;                 ProjectileMovementComponent->MaxSpeed = 3000.0f;                 ProjectileMovementComponent->bRotationFollowsVelocity = true;                 ProjectileMovementComponent->bShouldBounce = true;                 ProjectileMovementComponent->Bounciness = 0.3f;                 ProjectileMovementComponent->ProjectileGravityScale = 0.0f;             }                       if (!ProjectileMeshComponent)             {                 ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent"));                 static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'"));                 if (Mesh.Succeeded())                 {                     ProjectileMeshComponent->SetStaticMesh(Mesh.Object);                 }                           static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'"));                 if (Material.Succeeded())                 {                     ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent);                 }                 ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance);                 ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f));                 ProjectileMeshComponent->SetupAttachment(RootComponent);             }                       // Delete the projectile after 3 seconds.             InitialLifeSpan = 3.0f;         }                   // Called when the game starts or when spawned         void AFPSProjectile::BeginPlay()         {             Super::BeginPlay();                      }                   // Called every frame         void AFPSProjectile::Tick(float DeltaTime)         {             Super::Tick(DeltaTime);                   }          		// Function that initializes the projectile's velocity in the shoot direction.         void AFPSProjectile::FireInDirection(const FVector& ShootDirection)         {             ProjectileMovementComponent->Velocity = ShootDirection * ProjectileMovementComponent->InitialSpeed;         } 		         void AFPSProjectile::OnHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComponent, FVector NormalImpulse, const FHitResult& Hit)         {             if (OtherActor != nullptr && OtherActor != this && OtherComponent != nullptr && OtherComponent->IsSimulatingPhysics())             {                 OtherComponent->AddImpulseAtLocation(ProjectileMovementComponent->Velocity * 100.0f, Hit.ImpactPoint);             }             Destroy();         }`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectile.h" // Sets default values AFPSProjectile::AFPSProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; if (!RootComponent) { RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("ProjectileSceneComponent")); } if (!CollisionComponent) { // Use a sphere as a simple collision representation. CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); // Set the sphere's collision profile name to "Projectile". CollisionComponent->BodyInstance.SetCollisionProfileName(TEXT("Projectile")); // Event called when component hits something. CollisionComponent->OnComponentHit.AddDynamic(this, &AFPSProjectile::OnHit); // Set the sphere's collision radius. CollisionComponent->InitSphereRadius(15.0f); // Set the root component to be the collision component. RootComponent = CollisionComponent; } if (!ProjectileMovementComponent) { // Use this component to drive this projectile's movement. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovementComponent")); ProjectileMovementComponent->SetUpdatedComponent(CollisionComponent); ProjectileMovementComponent->InitialSpeed = 3000.0f; ProjectileMovementComponent->MaxSpeed = 3000.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->bShouldBounce = true; ProjectileMovementComponent->Bounciness = 0.3f; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; } if (!ProjectileMeshComponent) { ProjectileMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("ProjectileMeshComponent")); static ConstructorHelpers::FObjectFinder<UStaticMesh>Mesh(TEXT("'/Game/Sphere.Sphere'")); if (Mesh.Succeeded()) { ProjectileMeshComponent->SetStaticMesh(Mesh.Object); } static ConstructorHelpers::FObjectFinder<UMaterial>Material(TEXT("'/Game/SphereMaterial.SphereMaterial'")); if (Material.Succeeded()) { ProjectileMaterialInstance = UMaterialInstanceDynamic::Create(Material.Object, ProjectileMeshComponent); } ProjectileMeshComponent->SetMaterial(0, ProjectileMaterialInstance); ProjectileMeshComponent->SetRelativeScale3D(FVector(0.09f, 0.09f, 0.09f)); ProjectileMeshComponent->SetupAttachment(RootComponent); } // Delete the projectile after 3 seconds. InitialLifeSpan = 3.0f; } // Called when the game starts or when spawned void AFPSProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFPSProjectile::Tick(float DeltaTime) { Super::Tick(DeltaTime); } // Function that initializes the projectile's velocity in the shoot direction. void AFPSProjectile::FireInDirection(const FVector& ShootDirection) { ProjectileMovementComponent->Velocity = ShootDirection \* ProjectileMovementComponent->InitialSpeed; } void AFPSProjectile::OnHit(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComponent, FVector NormalImpulse, const FHitResult& Hit) { if (OtherActor != nullptr && OtherActor != this && OtherComponent != nullptr && OtherComponent->IsSimulatingPhysics()) { OtherComponent->AddImpulseAtLocation(ProjectileMovementComponent->Velocity \* 100.0f, Hit.ImpactPoint); } Destroy(); }

FPSCharacter.h

```
        `// Copyright Epic Games, Inc. All Rights Reserved.                   #pragma once                   #include "CoreMinimal.h"         #include "GameFramework/Character.h"         #include "Camera/CameraComponent.h"         #include "Components/CapsuleComponent.h"         #include "FPSProjectile.h"         #include "FPSCharacter.generated.h"                   UCLASS()         class FPSPROJECT_API AFPSCharacter : public ACharacter         {             GENERATED_BODY()                   public:             // Sets default values for this character's properties             AFPSCharacter();                   protected:             // Called when the game starts or when spawned             virtual void BeginPlay() override;                       // Projectile class to spawn.             UPROPERTY(EditAnywhere, Category = Projectile)             TSubclassOf<class AFPSProjectile> ProjectileClass;                   public:	             // Called every frame             virtual void Tick(float DeltaTime) override;                       // Called to bind functionality to input             virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;                       // Handles input for moving forward and backward.             UFUNCTION()             void MoveForward(float Value);                       // Handles input for moving right and left.             UFUNCTION()             void MoveRight(float Value);                       // Sets jump flag when key is pressed.             UFUNCTION()             void StartJump();                       // Clears jump flag when key is released.             UFUNCTION()             void StopJump();                       // FPS camera             UPROPERTY(VisibleAnywhere)             UCameraComponent* FPSCameraComponent;                       // First-person mesh (arms), visible only to the owning player.             UPROPERTY(VisibleDefaultsOnly, Category = Mesh)             USkeletalMeshComponent* FPSMesh; 			 			// Function that fires projectiles.             UFUNCTION()             void Fire();                       // Gun muzzle offset from the camera location.             UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Gameplay)             FVector MuzzleOffset;         };`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Character.h" #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h" #include "FPSProjectile.h" #include "FPSCharacter.generated.h" UCLASS() class FPSPROJECT\_API AFPSCharacter : public ACharacter { GENERATED\_BODY() public: // Sets default values for this character's properties AFPSCharacter(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; // Projectile class to spawn. UPROPERTY(EditAnywhere, Category = Projectile) TSubclassOf<class AFPSProjectile> ProjectileClass; public: // Called every frame virtual void Tick(float DeltaTime) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) override; // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value); // Sets jump flag when key is pressed. UFUNCTION() void StartJump(); // Clears jump flag when key is released. UFUNCTION() void StopJump(); // FPS camera UPROPERTY(VisibleAnywhere) UCameraComponent\* FPSCameraComponent; // First-person mesh (arms), visible only to the owning player. UPROPERTY(VisibleDefaultsOnly, Category = Mesh) USkeletalMeshComponent\* FPSMesh; // Function that fires projectiles. UFUNCTION() void Fire(); // Gun muzzle offset from the camera location. UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Gameplay) FVector MuzzleOffset; };

FPSCharacter.cpp

```
        `// Copyright Epic Games, Inc. All Rights Reserved.                            #include "FPSCharacter.h"                   // Sets default values         AFPSCharacter::AFPSCharacter()         {             // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.             PrimaryActorTick.bCanEverTick = true;                       // Create a first person camera component.             FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));             check(FPSCameraComponent != nullptr);                          // Attach the camera component to our capsule component.             FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent()));                          // Position the camera slightly above the eyes.             FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight));                          // Enable the Pawn to control camera rotation.             FPSCameraComponent->bUsePawnControlRotation = true;                          // Create a first person mesh component for the owning player.             FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh"));             check(FPSMesh != nullptr);                          // Only the owning player sees this mesh.             FPSMesh->SetOnlyOwnerSee(true);                       //Attach the FPS mesh to the FPS Camera.             FPSMesh->SetupAttachment(FPSCameraComponent);                          //Disable some environmental shadows to preserve the illusion of having a single mesh.             FPSMesh->bCastDynamicShadow = false;             FPSMesh->CastShadow = false;                          // The owning player doesn't see the regular (third-person) body mesh.             GetMesh()->SetOwnerNoSee(true);         }           		// Called when the game starts or when spawned 		void AFPSCharacter::BeginPlay() 		{ 			Super::BeginPlay(); 			 			check(GEngine != nullptr);  			// Display a debug message for five seconds.  			// The -1 "Key" value argument prevents the message from being updated or refreshed. 			GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); 		}                   // Called every frame         void AFPSCharacter::Tick(float DeltaTime)         {             Super::Tick(DeltaTime);                   }                   // Called to bind functionality to input         void AFPSCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)         {             Super::SetupPlayerInputComponent(PlayerInputComponent);                       // Set up "movement" bindings.             PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);             PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);                       // Set up "look" bindings.             PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput);             PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);                       // Set up "action" bindings.             PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &AFPSCharacter::StartJump);             PlayerInputComponent->BindAction("Jump", IE_Released, this, &AFPSCharacter::StopJump);             PlayerInputComponent->BindAction("Fire", IE_Pressed, this, &AFPSCharacter::Fire);         }                   void AFPSCharacter::MoveForward(float Value)         {             // Find out which way is "forward" and record that the player wants to move that way.             FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);             AddMovementInput(Direction, Value);         }                   void AFPSCharacter::MoveRight(float Value)         {             // Find out which way is "right" and record that the player wants to move that way.             FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);             AddMovementInput(Direction, Value);         }                   void AFPSCharacter::StartJump()         {             bPressedJump = true;         }                   void AFPSCharacter::StopJump()         {             bPressedJump = false;         }                   void AFPSCharacter::Fire()         {             // Attempt to fire a projectile.             if (ProjectileClass)             {                 // Get the camera transform.                 FVector CameraLocation;                 FRotator CameraRotation;                 GetActorEyesViewPoint(CameraLocation, CameraRotation);                                  // Set MuzzleOffset to spawn projectiles slightly in front of the camera.                 MuzzleOffset.Set(100.0f, 0.0f, 0.0f);                           // Transform MuzzleOffset from camera space to world space.                 FVector MuzzleLocation = CameraLocation + FTransform(CameraRotation).TransformVector(MuzzleOffset);                           // Skew the aim to be slightly upwards.                  FRotator MuzzleRotation = CameraRotation;                 MuzzleRotation.Pitch += 10.0f;                           UWorld* World = GetWorld();                 if (World)                 {                     FActorSpawnParameters SpawnParams;                     SpawnParams.Owner = this;                     SpawnParams.Instigator = GetInstigator();                               // Spawn the projectile at the muzzle.                     AFPSProjectile* Projectile = World->SpawnActor<AFPSProjectile>(ProjectileClass, MuzzleLocation, MuzzleRotation, SpawnParams);                     if (Projectile)                     {                         // Set the projectile's initial trajectory.                         FVector LaunchDirection = MuzzleRotation.Vector();                         Projectile->FireInDirection(LaunchDirection);                     }                                      }             }         }`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #include "FPSCharacter.h" // Sets default values AFPSCharacter::AFPSCharacter() { // Set this character to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Create a first person camera component. FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); check(FPSCameraComponent != nullptr); // Attach the camera component to our capsule component. FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent())); // Position the camera slightly above the eyes. FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight)); // Enable the Pawn to control camera rotation. FPSCameraComponent->bUsePawnControlRotation = true; // Create a first person mesh component for the owning player. FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh")); check(FPSMesh != nullptr); // Only the owning player sees this mesh. FPSMesh->SetOnlyOwnerSee(true); //Attach the FPS mesh to the FPS Camera. FPSMesh->SetupAttachment(FPSCameraComponent); //Disable some environmental shadows to preserve the illusion of having a single mesh. FPSMesh->bCastDynamicShadow = false; FPSMesh->CastShadow = false; // The owning player doesn't see the regular (third-person) body mesh. GetMesh()->SetOwnerNoSee(true); } // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() { Super::BeginPlay(); check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); } // Called every frame void AFPSCharacter::Tick(float DeltaTime) { Super::Tick(DeltaTime); } // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight); // Set up "look" bindings. PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput); PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput); // Set up "action" bindings. PlayerInputComponent->BindAction("Jump", IE\_Pressed, this, &AFPSCharacter::StartJump); PlayerInputComponent->BindAction("Jump", IE\_Released, this, &AFPSCharacter::StopJump); PlayerInputComponent->BindAction("Fire", IE\_Pressed, this, &AFPSCharacter::Fire); } void AFPSCharacter::MoveForward(float Value) { // Find out which way is "forward" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); } void AFPSCharacter::MoveRight(float Value) { // Find out which way is "right" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y); AddMovementInput(Direction, Value); } void AFPSCharacter::StartJump() { bPressedJump = true; } void AFPSCharacter::StopJump() { bPressedJump = false; } void AFPSCharacter::Fire() { // Attempt to fire a projectile. if (ProjectileClass) { // Get the camera transform. FVector CameraLocation; FRotator CameraRotation; GetActorEyesViewPoint(CameraLocation, CameraRotation); // Set MuzzleOffset to spawn projectiles slightly in front of the camera. MuzzleOffset.Set(100.0f, 0.0f, 0.0f); // Transform MuzzleOffset from camera space to world space. FVector MuzzleLocation = CameraLocation + FTransform(CameraRotation).TransformVector(MuzzleOffset); // Skew the aim to be slightly upwards. FRotator MuzzleRotation = CameraRotation; MuzzleRotation.Pitch += 10.0f; UWorld\* World = GetWorld(); if (World) { FActorSpawnParameters SpawnParams; SpawnParams.Owner = this; SpawnParams.Instigator = GetInstigator(); // Spawn the projectile at the muzzle. AFPSProjectile\* Projectile = World->SpawnActor<AFPSProjectile>(ProjectileClass, MuzzleLocation, MuzzleRotation, SpawnParams); if (Projectile) { // Set the projectile's initial trajectory. FVector LaunchDirection = MuzzleRotation.Vector(); Projectile->FireInDirection(LaunchDirection); } } } }

FPSHUD.h

```
        `// Copyright Epic Games, Inc. All Rights Reserved.                   #pragma once                   #include "CoreMinimal.h"         #include "GameFramework/HUD.h"         #include "Engine/Canvas.h"         #include "FPSHUD.generated.h"                   /**          *           */         UCLASS()         class FPSPROJECT_API AFPSHUD : public AHUD         {             GENERATED_BODY()                      protected:             // This will be drawn at the center of the screen.             UPROPERTY(EditDefaultsOnly)             UTexture2D* CrosshairTexture; 		 		public:             // Primary draw call for the HUD.             virtual void DrawHUD() override;         };`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/HUD.h" #include "Engine/Canvas.h" #include "FPSHUD.generated.h" /\*\* \* \*/ UCLASS() class FPSPROJECT\_API AFPSHUD : public AHUD { GENERATED\_BODY() protected: // This will be drawn at the center of the screen. UPROPERTY(EditDefaultsOnly) UTexture2D\* CrosshairTexture; public: // Primary draw call for the HUD. virtual void DrawHUD() override; };

FPSHUD.cpp

```
        `// Copyright Epic Games, Inc. All Rights Reserved.                            #include "FPSHUD.h"                   void AFPSHUD::DrawHUD()         {             Super::DrawHUD();                       if (CrosshairTexture)             {                 // Find the center of our canvas.                 FVector2D Center(Canvas->ClipX * 0.5f, Canvas->ClipY * 0.5f);                           // Offset by half of the texture's dimensions so that the center of the texture aligns with the center of the Canvas.                 FVector2D CrossHairDrawPosition(Center.X - (CrosshairTexture->GetSurfaceWidth() * 0.5f), Center.Y - (CrosshairTexture->GetSurfaceHeight() * 0.5f));                           // Draw the crosshair at the centerpoint.                 FCanvasTileItem TileItem(CrossHairDrawPosition, CrosshairTexture->Resource, FLinearColor::White);                 TileItem.BlendMode = SE_BLEND_Translucent;                 Canvas->DrawItem(TileItem);             }         }`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #include "FPSHUD.h" void AFPSHUD::DrawHUD() { Super::DrawHUD(); if (CrosshairTexture) { // Find the center of our canvas. FVector2D Center(Canvas->ClipX \* 0.5f, Canvas->ClipY \* 0.5f); // Offset by half of the texture's dimensions so that the center of the texture aligns with the center of the Canvas. FVector2D CrossHairDrawPosition(Center.X - (CrosshairTexture->GetSurfaceWidth() \* 0.5f), Center.Y - (CrosshairTexture->GetSurfaceHeight() \* 0.5f)); // Draw the crosshair at the centerpoint. FCanvasTileItem TileItem(CrossHairDrawPosition, CrosshairTexture->Resource, FLinearColor::White); TileItem.BlendMode = SE\_BLEND\_Translucent; Canvas->DrawItem(TileItem); } }

Congratulations! You've learned how to:

✓ Add Projectiles to your Game  
✓ Implement Shooting  
✓ Set-up Projectile Collision and Lifetime  
✓ Get your Projectiles to Interact with the World  
✓ Add Crosshairs to your Viewport

You're now ready to learn how to animate your character in the next section.