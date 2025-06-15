# Implement a Projectile

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/implement-a-projectile-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/implement-a-projectile-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:52

---

## Before You Begin

Ensure you’ve completed the following objectives in the previous section, [Equip Your Character](https://dev.epicgames.com/documentation/en-us/unreal-engine/equip-your-character-with-cplusplus-tools): 

-   Created a respawning pickup item and added it to your level
    
-   Created an equippable dart launcher for your character to hold and use
    

## Basic Projectiles

Your character can hold your dart launcher, and your tool has control bindings to use it, but it’s not quite living up to its name. In this section, you’ll implement projectile logic to make darts launch out from the equipped item. 

Unreal Engine has a **Projectile Movement** component class that you can add to an actor to turn it into a projectile. It includes many helpful variables, such as projectile speed, bounciness, and gravity scale.  

To handle the math of implementing projectiles, you’ll need to think about several things:

-   The initial transform, velocity, and direction of the projectile.
    
-   Whether you want to spawn projectiles from the center of the character or the tool they have equipped.
    
-   What behavior you want the projectile to exhibit when it collides with another object.
    

## Create a Projectile Base Class

You’ll first create a base projectile class, and then subclass from it to create unique projectiles for your tools. 

To start setting up a base projectile class, follow these steps:

1.  In the Unreal Editor, go to **Tools > New C++ Class**. Select **Actor** as the parent class and name the class `FirstPersonProjectile`. Click **Create Class**.
    
2.  In VS, go to `FirstPersonProjectile.h`. At the top of the file, forward declare both a `UProjectileMovementComponent` and a `USphereComponent`.
    
    You’ll use the sphere component to simulate collisions between the projectile and other objects.
    
    C++
    
    `// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "FirstPersonProjectile.generated.h"  class UProjectileMovementComponent; class USphereComponent;`
    
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include &quot;CoreMinimal.h&quot; #include &quot;GameFramework/Actor.h&quot; #include &quot;FirstPersonProjectile.generated.h&quot; class UProjectileMovementComponent; class USphereComponent;
    
    Copy full snippet(10 lines long)
    
3.  Add the `BlueprintType` and `Blueprintable` specifiers to expose this class to Blueprints:
    
    C++
    
    `UCLASS(BlueprintType, Blueprintable) class FIRSTPERSON_API AFirstPersonProjectile : public AActor`
    
    UCLASS(BlueprintType, Blueprintable) class FIRSTPERSON\_API AFirstPersonProjectile : public AActor
    
    Copy full snippet(2 lines long)
    
4.  Open `FirstPersonProjectile.cpp`, att the top of the file, add an include statement for `”GameFramework/ProjectileMovementComponent.h”` to include the projectile movement component class.
    

C++

`#include "FirstPersonProjectile.h" #include "GameFramework/ProjectileMovementComponent.h" #include "Components/SphereComponent.h"  // Sets default values AFirstPersonProjectile::AFirstPersonProjectile()`

#include "FirstPersonProjectile.h" #include "GameFramework/ProjectileMovementComponent.h" #include "Components/SphereComponent.h" // Sets default values AFirstPersonProjectile::AFirstPersonProjectile()

Copy full snippet(6 lines long)

### Implement Projectile Behavior When Hitting Objects

To make your projectile more realistic, you can make it exert some force (an impulse) on objects it hits. For example, if you are shooting at a physics-enabled block, the projectile would nudge the block along the ground. Then, remove the projectile after impact instead of letting it live out its default lifespan. Create an `OnHit()` function to implement this behavior.

To implement projectile on-hit behavior, follow these steps:  

1.  In `FirstPersonProjectile.h`, in the `public` section, define a `float` property named `PhysicsForce`.
    
    Give it a `UPROPERTY()` macro with `EditAnywhere`, `BlueprintReadOnly`, and `Category = “Projectile | Physics”`.
    
    This is the amount of force the projectile imparts when it hits something.
    
    C++
    
    `// The amount of force this projectile imparts on objects it collides with UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Projectile | Physics") float PhysicsForce = 100.0f;`
    
    // The amount of force this projectile imparts on objects it collides with UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = &quot;Projectile | Physics&quot;) float PhysicsForce = 100.0f;
    
    Copy full snippet(3 lines long)
    
2.  Define a `void` function `OnHit()`. This is a function from AActor called when the actor collides with another component or actor. It takes the following arguments:
    
    -   `HitComp`: The component that was hit.
        
    -   `OtherActor`: The actor that was hit.
        
    -   `OtherComp`: The component that created the hit (in this case, the projectile’s CollisionComponent).
        
    -   `NormalImpulse`: The normal impulse of the hit.
        
    -   `Hit`: A `FHitResult` reference that contains more data about the hit event such as time, distance, and location.
        
    
    C++
    
    `// Called when the projectile collides with an object UFUNCTION() void OnHit(UPrimitiveComponent* HitComp, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit);`
    
    // Called when the projectile collides with an object UFUNCTION() void OnHit(UPrimitiveComponent\* HitComp, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, FVector NormalImpulse, const FHitResult&amp; Hit);
    
    Copy full snippet(3 lines long)
    
3.  In `FirstPersonProjectile.cpp`, implement the `OnHit()` function you defined in your header file. Inside `OnHit()`, in an `if` statement, check that: 
    
    1.  `OtherActor` isn't null and isn't the projectile itself.
        
    2.  `OtherComp` isn't null and is also simulating physics.
        
    
    C++
    
    `void AFirstPersonProjectile::OnHit(UPrimitiveComponent* HitComp, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit) { 	// Only add impulse and destroy projectile if we hit a physics 	if ((OtherActor != nullptr) && (OtherActor != this) && (OtherComp != nullptr) && OtherComp->IsSimulatingPhysics()) 	{ 	} }`
    
    void AFirstPersonProjectile::OnHit(UPrimitiveComponent\* HitComp, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, FVector NormalImpulse, const FHitResult&amp; Hit) { // Only add impulse and destroy projectile if we hit a physics if ((OtherActor != nullptr) &amp;&amp; (OtherActor != this) &amp;&amp; (OtherComp != nullptr) &amp;&amp; OtherComp-&gt;IsSimulatingPhysics()) { } }
    
    Copy full snippet(7 lines long)
    
    This checks that the projectile hit an object that wasn’t itself and participates in physics.
    
4.  Inside the `if` statement, use `AddImpulseAtLocation()` to add an impulse to the `OtherComp` component.
    
    Pass this function the velocity of the projectile multiplied by the `PhysicsForce` and apply it at the location of the projectile actor.
    
    C++
    
    `if ((OtherActor != nullptr) && (OtherActor != this) && (OtherComp != nullptr) && OtherComp->IsSimulatingPhysics()) { 	OtherComp->AddImpulseAtLocation(GetVelocity() * PhysicsForce, GetActorLocation());  }`
    
    if ((OtherActor != nullptr) &amp;&amp; (OtherActor != this) &amp;&amp; (OtherComp != nullptr) &amp;&amp; OtherComp-&gt;IsSimulatingPhysics()) { OtherComp-&gt;AddImpulseAtLocation(GetVelocity() \* PhysicsForce, GetActorLocation()); }
    
    Copy full snippet(5 lines long)
    
    `AddImpulseAtLocation()` is a physics function in Unreal Engine that applies an instantaneous force (impulse) to a simulated physics object at a specific world-space location. It’s useful when you want to simulate an impact, like an explosion throwing something, a bullet hitting an object, or a door swinging open.
    
5.  Last, since this projectile hit another actor, remove the projector from the scene by calling `Destroy()`.
    

Your complete `OnHit()` function should look like the following:

C++

`void AFirstPersonProjectile::OnHit(UPrimitiveComponent* HitComp, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit) { 	// Only add impulse and destroy projectile if we hit a physics 	if ((OtherActor != nullptr) && (OtherActor != this) && (OtherComp != nullptr) && OtherComp->IsSimulatingPhysics()) 	{ 		OtherComp->AddImpulseAtLocation(GetVelocity() * PhysicsForce, GetActorLocation());  		Destroy(); 	} }`

void AFirstPersonProjectile::OnHit(UPrimitiveComponent\* HitComp, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, FVector NormalImpulse, const FHitResult& Hit) { // Only add impulse and destroy projectile if we hit a physics if ((OtherActor != nullptr) && (OtherActor != this) && (OtherComp != nullptr) && OtherComp->IsSimulatingPhysics()) { OtherComp->AddImpulseAtLocation(GetVelocity() \* PhysicsForce, GetActorLocation()); Destroy(); } }

Copy full snippet(10 lines long)

### Add the Projectile’s Mesh, Movement, Collision Components

Next, add a static mesh, projectile movement logic, and a collision sphere to your projectile and define how the projectile should move.

To add these components to your projectile, follow these steps:

1.  In `FirstPersonProjectile.h`, in the `public` section, declare a `TObjectPtr` to a `UStaticMeshComponent` named `ProjectileMesh`. This is the static mesh of the projectile in the world.
    
    Give it a `UPROPERTY()` macro with `EditAnywhere`, `BlueprintReadOnly`, and `Category = “Projectile | Mesh“`.
    
    C++
    
    `// Mesh of the projectile in the world  UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Projectile | Mesh") TObjectPtr<UStaticMeshComponent> ProjectileMesh;`
    
    // Mesh of the projectile in the world UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = &quot;Projectile | Mesh&quot;) TObjectPtr&lt;UStaticMeshComponent&gt; ProjectileMesh;
    
    Copy full snippet(3 lines long)
    
2.  In the `protected` section, declare:
    
    -   A `TObjectPtr` to a `USphereComponent` named `CollisionComponent`.
        
    -   A `TObjectPtr` to a `UProjectileMovementComponent` named `ProjectileMovement`.
        
    
    Give both of these a `UPROPERTY()` macro with `VisibleAnywhere`, `BlueprintReadOnly`, and `Category = “Projectile | Components”`.
    
    C++
    
    `// Sphere collision component  UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Projectile | Components") TObjectPtr<USphereComponent> CollisionComponent;  // Projectile movement component UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Projectile | Components") TObjectPtr<UProjectileMovementComponent> ProjectileMovement;`
    
    // Sphere collision component UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = &quot;Projectile | Components&quot;) TObjectPtr&lt;USphereComponent&gt; CollisionComponent; // Projectile movement component UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = &quot;Projectile | Components&quot;) TObjectPtr&lt;UProjectileMovementComponent&gt; ProjectileMovement;
    
    Copy full snippet(7 lines long)
    
    The ProjectileMovementComponent handles movement logic for you. It calculates where its parent Actor should go based on velocity, gravity, and other variables. Then, during `tick`, it applies the movement to the projectile.
    
3.  In `FirstPersonProjectile.cpp`, in the `AFirstPersonProjectile()` constructor function, create default subobjects for the projectile’s mesh, collision, and projectile movement components. Then, attach the projectile mesh to the collision component.
    
    C++
    
    ```code
    `// Sets default values AFirstPersonProjectile::AFirstPersonProjectile() {  	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;  	// Use a sphere as a simple collision representation 	CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("CollisionComponent")); 	check(CollisionComponent != nullptr);`
    
    
    ```
    
    Expand codeCopy full snippet(20 lines long)
    
4.  Call `InitSphereRadius()` to initialize the `CollisionComponent` with a radius of `5.0f`.
    
5.  Set the name of the collision component’s collision profile to `”Projectile”` using `BodyInstance.SetCollisionProfileName()`.
    
    In Unreal Editor, your collision profiles are stored under **Project Settings** \> **Engine** \> **Collision**, and you can define up to 18 custom collision profiles to use in code. The default behavior of this ”Projectile” collision profile is **Block**, and this creates collisions on any object it collides with.
    
    C++
    
    `CollisionComponent->InitSphereRadius(5.0f);  // Set the collision profile to the "Projectile" collision preset CollisionComponent->BodyInstance.SetCollisionProfileName("Projectile");`
    
    CollisionComponent-&gt;InitSphereRadius(5.0f); // Set the collision profile to the &quot;Projectile&quot; collision preset CollisionComponent-&gt;BodyInstance.SetCollisionProfileName(&quot;Projectile&quot;);
    
    Copy full snippet(5 lines long)
    
6.  You defined an `OnHit()` function earlier to activate when the projectile hits something, but you need a way to notify when that collision occurs. To do this, use the `AddDynamic()` macro to subscribe a function to `OnComponentHitEvent` in `CollisionComponent`. Pass this macro the `OnHit()` function.
    
    C++
    
    `// Set up a notification for when this component hits something blocking CollisionComponent->OnComponentHit.AddDynamic(this, &AFirstPersonProjectile::OnHit);`
    
    // Set up a notification for when this component hits something blocking CollisionComponent-&gt;OnComponentHit.AddDynamic(this, &amp;AFirstPersonProjectile::OnHit);
    
    Copy full snippet(2 lines long)
    
7.  Set the `CollisionComponent` as the projectile’s `RootComponent` and as the `UpdatedComponent` for the movement component to track.
    
    C++
    
    `// Set as root component RootComponent = CollisionComponent;  ProjectileMovement->UpdatedComponent = CollisionComponent;`
    
    // Set as root component RootComponent = CollisionComponent; ProjectileMovement-&gt;UpdatedComponent = CollisionComponent;
    
    Copy full snippet(4 lines long)
    
8.  Initialize the `ProjectileMovement` component with the following values:
    
    -   `InitialSpeed`: The initial speed of the projectile when it spawns. Set this to `3000.0f`.
        
    -   `MaxSpeed`: The maximum speed of the projectile. Set this to `3000.0f`.
        
    -   `bRotationFollowVelocity`: Whether the object should rotate to make the direction of its velocity. For example, how a paper airplane dips up and down as it rises and falls. Set this to `true`.
        
    -   `bShouldBounce`: Whether the projectile should bounce off obstacles. Set this to `true`.
        
    
    C++
    
    `ProjectileMovement->UpdatedComponent = CollisionComponent; ProjectileMovement->InitialSpeed = 3000.f; ProjectileMovement->MaxSpeed = 3000.f; ProjectileMovement->bRotationFollowsVelocity = true; ProjectileMovement->bShouldBounce = true;`
    
    ProjectileMovement-&gt;UpdatedComponent = CollisionComponent; ProjectileMovement-&gt;InitialSpeed = 3000.f; ProjectileMovement-&gt;MaxSpeed = 3000.f; ProjectileMovement-&gt;bRotationFollowsVelocity = true; ProjectileMovement-&gt;bShouldBounce = true;
    
    Copy full snippet(5 lines long)
    

### Set the Projectile’s Lifespan

By default, you’ll make the projectile disappear a few seconds after firing it. However, once you derive your projectile Blueprints in the editor, you can experiment with changing or removing this default time to try filling your level up with foam darts!

To make the projectile disappear after a number of seconds, follow these steps:

1.  In `FirstPersonProjectile.h`, in the `public` section, declare a float named `ProjectileLifespan`.
    
    Give it a `UPROPERTY()` macro with `EditAnywhere`, `BlueprintReadOnly`, and `Category = “Projectile | Lifespan”`.
    
    This is the lifespan of the projectile in seconds.
    
    C++
    
    `// Despawn after 5 seconds by default UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Projectile | Lifespan") float ProjectileLifespan = 5.0f;`
    
    // Despawn after 5 seconds by default UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = &quot;Projectile | Lifespan&quot;) float ProjectileLifespan = 5.0f;
    
    Copy full snippet(3 lines long)
    
2.  In `FirstPersonProjectile.cpp`, at the end of the `AFirstPersonProjectile()` constructor function, set the `InitialLifeSpan` of the projectile to `ProjectileLifespan` to make it disappear after five seconds.
    
    C++
    
    `// Disappear after 5.0 seconds by default. 	InitialLifeSpan = ProjectileLifespan;`
    
    // Disappear after 5.0 seconds by default. InitialLifeSpan = ProjectileLifespan;
    
    Copy full snippet(2 lines long)
    
    `InitialLifeSpan` is a property inherited from AActor. It’s a float that sets how long the Actor lives before dying. A value of `0` means the Actor lives until the game stops.
    

  Your complete `FirstPersonProjectile.h` should look like the following:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "FirstPersonProjectile.generated.h"  class UProjectileMovementComponent; class USphereComponent;`

```

Expand codeCopy full snippet(54 lines long)

Your complete `AFirstPersonProjectile` constructor function should look like the following:

C++

```code
`// Sets default values AFirstPersonProjectile::AFirstPersonProjectile() {  	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;  	// Use a sphere as a simple collision representation 	CollisionComponent = CreateDefaultSubobject<USphereComponent>(TEXT("CollisionComponent")); 	check(CollisionComponent != nullptr);`


```

Expand codeCopy full snippet(41 lines long)

## Get the Character Camera Direction

Projectiles should spawn from the dart launcher itself, so you’ll need to do some math to know where the dart launcher is and where it’s pointing. Since the launcher is attached to the player character, these values are going to change based on where the character is and where they’re looking. 

Your first-person character contains some of the positional information you need to launch a dart, so start by modifying your Character class to capture that information with a line trace and return the result.

To use a trace to get the information you need from your character, follow these steps:

1.  In VS, open your Character’s `.h` and `.cpp` files.
    
2.  In the `.h` file, in the `public` section, declare a new function named `GetCameraTargetLocation()`  that returns an `FVector`. This function will return the location in the world that the character is looking at.
    
    C++
    
    `// Returns the location in the world the character is looking at UFUNCTION() FVector GetCameraTargetLocation();`
    
    // Returns the location in the world the character is looking at UFUNCTION() FVector GetCameraTargetLocation();
    
    Copy full snippet(3 lines long)
    
3.  In your Character's `.cpp` file, implement the `GetCameraTargetLocation()` function. Start by declaring an FVector named `TargetPosition` to return.
    
4.  Create a pointer to `UWorld` by calling `GetWorld()`.
    
    C++
    
    `// The target position to return FVector TargetPosition;  UWorld* const World = GetWorld();`
    
    // The target position to return FVector TargetPosition; UWorld\* const World = GetWorld();
    
    Copy full snippet(4 lines long)
    
5.  Add an `if` statement to check that `World` isn’t null. In the `if` statement, declare a `FHitResult` named `Hit`.
    
    C++
    
    `if (World != nullptr) { 	// The result of the line trace FHitResult Hit;`
    
    if (World != nullptr) { // The result of the line trace FHitResult Hit;
    
    Copy full snippet(4 lines long)
    
    `FHitResult` is a struct in UE that stores information about the result of a collision query, including the Actor or component that was hit and where you hit it.
    
6.  To find the point that your character is looking at, you’re going to simulate a line trace along the vector the character is looking down to some distant point. If the line trace collides with an object, you know where in the world your character is looking.
    
    Declare two const FVector values named TraceStart and TraceEnd:
    
    1.  Set `TraceStart` to the location of the `FirstPersonCameraComponent`.  
        
    2.  Set `TraceEnd` to `TraceStart` plus the forward vector of the camera component multiplied by a very large number. This ensures that the trace will go far enough to collide with most objects in your world as long as your character isn’t staring at the sky. (If the character is looking at the sky, `TraceEnd` is the terminal point of the line trace.)
        
        C++
        
        `// Simulate a line trace from the character along the vector they're looking down const FVector TraceStart = FirstPersonCameraComponent->GetComponentLocation(); const FVector TraceEnd = TraceStart + FirstPersonCameraComponent->GetForwardVector() * 10000.0;`
        
        // Simulate a line trace from the character along the vector they&#39;re looking down const FVector TraceStart = FirstPersonCameraComponent-&gt;GetComponentLocation(); const FVector TraceEnd = TraceStart + FirstPersonCameraComponent-&gt;GetForwardVector() \* 10000.0;
        
        Copy full snippet(3 lines long)
        
7.  Call `LineTraceSingleByChannel()` from the `UWorld` to simulate the trace. Pass it `Hit`, `TraceStart`, `TraceEnd`, and an `ECollisionChannel::ECC_Visibility`.
    
    This simulates a line trace from `TraceStart` to `TraceEnd`, colliding with any visible objects and storing the result of the trace in `Hit`. `ECollisionChannel::ECC_Visibility` is the channel to use for tracing, and these channels define what types of objects your trace should try to hit. Use `ECC_Visibility` for line-of-sight camera checks.
    
    C++
    
    `World->LineTraceSingleByChannel(Hit, TraceStart, TraceEnd, ECollisionChannel::ECC_Visibility);`
    
    World-&gt;LineTraceSingleByChannel(Hit, TraceStart, TraceEnd, ECollisionChannel::ECC\_Visibility);
    
    Copy full snippet(1 line long)
    
    The `Hit` value now contains information about the hit result, such as the location and normal of the impact. It also knows if the hit was a result of an object collision. The location of impact (or the end point of the trace line) is the camera target location to return.  
    
8.  Use a ternary operator to set `TargetPosition` to either the `Hit.ImpactPoint` if the hit was a blocking hit and `Hit.TraceEnd` if not. Then, return the `TargetPosition`.
    
    C++
    
    	`TargetPosition = Hit.bBlockingHit ? Hit.ImpactPoint : Hit.TraceEnd;  }  return TargetPosition;`
    
    TargetPosition = Hit.bBlockingHit ? Hit.ImpactPoint : Hit.TraceEnd; } return TargetPosition;
    
    Copy full snippet(5 lines long)
    

Your complete `GetCameraTargetLocation()` function should look like the following:

C++

```code
`FVector AADventureCharacter::GetCameraTargetLocation() { 	// The target position to return 	FVector TargetPosition;  	UWorld* const World = GetWorld(); 	if (World != nullptr) 	{ 		// The result of the line trace 		FHitResult Hit;`

```

Expand codeCopy full snippet(22 lines long)

## Spawn Projectiles with DartLauncher::Use()

Now that you have a way to know where the character is looking, you can implement the rest of the projectile logic in your dart launcher’s `Use()` function. You’ll get the location and direction to launch the projectile, then spawn the projectile. 

To get the location and rotation the projectile should spawn at, follow these steps:

1.  In `DartLauncher.h`, at the top of the file, add a forward declaration for `AFirstPersonProjectile`.
    
2.  In the `public` section, declare a `TSubclassOf<AFirstPersonProjectile>` property named ProjectileClass. This will be the projectile that the dart launcher spawns. Give this the `UPROPERTY()` macro with `EditAnywhere` and `Category = Projectile`.
    
    `DartLauncher.h` should now look like the following:
    
    C++
    
    ```code
    `// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "AdventureGame/EquippableToolBase.h" #include "AdventureGame/FirstPersonProjectile.h" #include "DartLauncher.generated.h"  class AFirstPersonProjectile;`
    
    ```
    
    Expand codeCopy full snippet(33 lines long)
    
3.  `DartLauncher.cpp`, add an include statement for `”Kismet/KismetMathLibrary.h”`. Projectile math can be complicated, and this file includes several handy functions you’ll use for launching projectiles.
    
    C++
    
    `#include "DartLauncher.h" #include "Kismet/KismetMathLibrary.h" #include "AdventureGame/AdventureCharacter.h"`
    
    #include &quot;DartLauncher.h&quot; #include &quot;Kismet/KismetMathLibrary.h&quot; #include &quot;AdventureGame/AdventureCharacter.h&quot;
    
    Copy full snippet(3 lines long)
    
4.  Start implementing DartLauncher’s `Use()` function:
    
    1.  Get the `UWorld` by calling `GetWorld()`.
        
    2.  Add an `if` statement to check that `World` and the `ProjectileClass` are not null.
        
    3.  In the `if` statement, get the position the character is looking at by calling `OwningCharacter->GetCameraTargetLocation()`.  
        
    
    C++
    
    `void ADartLauncher::Use() {    UWorld* const World = GetWorld();   if (World != nullptr && ProjectileClass != nullptr)   {     FVector TargetPosition = OwningCharacter->GetCameraTargetLocation();   }  }`
    
    void ADartLauncher::Use() { UWorld\* const World = GetWorld(); if (World != nullptr &amp;&amp; ProjectileClass != nullptr) { FVector TargetPosition = OwningCharacter-&gt;GetCameraTargetLocation(); } }
    
    Copy full snippet(10 lines long)
    
5.  Although you want to spawn projectiles from the tool the character is holding, you might not want to spawn them directly from the center of the object. The dart launcher’s `SKM_Pistol` mesh has a ”Muzzle” socket you can use to set a precise spawn point for your darts.   
    
    Declare a new `FVector` named `SocketLocation` and set it to the result of calling `GetSocketLocation(“Muzzle”)` on the `ToolMeshComponent`.  
    
    C++
    
    `// Get the correct socket to spawn the projectile from FVector SocketLocation = ToolMeshComponent->GetSocketLocation("Muzzle");`
    
    // Get the correct socket to spawn the projectile from FVector SocketLocation = ToolMeshComponent-&gt;GetSocketLocation(&quot;Muzzle&quot;);
    
    Copy full snippet(2 lines long)
    
6.  Next, declare a `FRotator` named `SpawnRotation`. This is the rotation (pitch, yaw, and roll values) of the projectile as it spawns.  
    
    Set this to the result of calling `FindLookAtRotation()` from the kismet math library, passing the `SocketLocation` and `TargetPosition` you got from the player character.  
    
    C++
    
    `FRotator SpawnRotation = UKismetMathLibrary::FindLookAtRotation(SocketLocation, TargetPosition);`
    
    FRotator SpawnRotation = UKismetMathLibrary::FindLookAtRotation(SocketLocation, TargetPosition);
    
    Copy full snippet(1 line long)
    
    `FindLookAtRotation` calculates and returns the rotation you’d need at `SocketLocation` to face `TargetPosition`.  
    
7.  Declare a `FVector` named `SpawnLocation`, and set it to the result of adding the `SocketLocation` and the forward vector of the `SpawnRotation` multiplied by `10.0`.  
    
    The muzzle socket isn’t quite at the front of the launcher, so you’ll need to multiply the vector by an offset to get the projectile firing from the right location.
    
    C++
    
    `FVector SpawnLocation = SocketLocation + UKismetMathLibrary::GetForwardVector(SpawnRotation) * 10.0;`
    
    FVector SpawnLocation = SocketLocation + UKismetMathLibrary::GetForwardVector(SpawnRotation) \* 10.0;
    
    Copy full snippet(1 line long)
    

Now that you’ve got a location and rotation, you’re ready to spawn the projectile. 

To spawn a projectile, follow these steps:

1.  Still in the `Use()` function, declare a `FActorSpawnParameters` named `ActorSpawnParams`. This class includes information about where and how to spawn the actor.
    
    C++
    
    `//Set Spawn Collision Handling Override FActorSpawnParameters ActorSpawnParams;`
    
    //Set Spawn Collision Handling Override FActorSpawnParameters ActorSpawnParams;
    
    Copy full snippet(2 lines long)
    
2.  Set the `SpawnCollisionHandlingOverride` value in `ActorSpawnParams` to `ESpawnActorCollisionHandlingMethod::AdjustIfPossibleButDontSpawnIfColliding`.
    
    This tries to find a place to spawn the projectile where it isn’t colliding with another Actor (such as inside a wall) and won’t spawn it if a suitable location isn’t found.
    
    C++
    
    `ActorSpawnParams.SpawnCollisionHandlingOverride = ESpawnActorCollisionHandlingMethod::AdjustIfPossibleButDontSpawnIfColliding;`
    
    ActorSpawnParams.SpawnCollisionHandlingOverride = ESpawnActorCollisionHandlingMethod::AdjustIfPossibleButDontSpawnIfColliding;
    
    Copy full snippet(1 line long)
    
3.  Use `SpawnActor()` to spawn the projectile at the muzzle of the dart launcher, passing `ProjectileClass`, `SpawnLocation`, `SpawnRotation`, and `ActorSpawnParams`.
    
    C++
    
    `// Spawn the projectile at the muzzle World->SpawnActor<AFirstPersonProjectile>(ProjectileClass, SpawnLocation, SpawnRotation, ActorSpawnParams);`
    
    // Spawn the projectile at the muzzle World-&gt;SpawnActor&lt;AFirstPersonProjectile&gt;(ProjectileClass, SpawnLocation, SpawnRotation, ActorSpawnParams);
    
    Copy full snippet(2 lines long)
    

Your complete `Use()` function should now look like the following:

C++

```code
`void ADartLauncher::Use() { 	GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Using the dart launcher!"));  	UWorld* const World = GetWorld(); 	if (World != nullptr && ProjectileClass != nullptr) 	{ 		FVector TargetPosition = OwningCharacter->GetCameraTargetLocation(); 			 		// Get the correct socket to spawn the projectile from`

```

Expand codeCopy full snippet(22 lines long)

## Derive a Foam Dart Class and Blueprint

Now that all the spawning logic is done, it’s time to build a real projectile! Your dart launcher class needs a subclass of `AFirstPersonProjectile` to launch, so you’ll need to build one in code to use in your level. 

To derive a foam dart projectile class to use in-game, follow these steps:

1.  In Unreal Editor, go to **Tools > New C++ Class**. 
    
2.  Go to **All Classes**, search for and select **First Person Projectile** as the parent class, and name the class `FoamDart`. Click **Create Class**.  
    
    [![](https://dev.epicgames.com/community/api/documentation/image/3260754a-e6c9-488d-a213-476f51aca730?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3260754a-e6c9-488d-a213-476f51aca730?resizing_type=fit)
    
3.  In VS, leave these files as-is, save your code, and compile it.
    

In this tutorial, you won’t be implementing any custom projectile code beyond what you defined in `FirstPersonProjectile`, but you can modify the `FoamDart` class on your own to suit the needs of your project. For example, you could try making the dart projectiles stick to objects instead of disappearing or bouncing around. 

To create a foam dart Blueprint, follow these steps:

1.  In Unreal Editor, create a Blueprint class based on **FoamDart** and name it `BP_FoamDart`. Save this in your `FirstPerson/Blueprints/Tools` folder.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/1615e276-bbd2-4765-8bd6-bcfd5c568311?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1615e276-bbd2-4765-8bd6-bcfd5c568311?resizing_type=fit)
    
2.  With the Blueprint open, select the **Projectile Mesh** component and set the **Static Mesh** to **SM\_FoamBullet**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/68b69db0-cd4f-47ba-a7c7-3782ea05d3d9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/68b69db0-cd4f-47ba-a7c7-3782ea05d3d9?resizing_type=fit)
    
3.  Save and compile your Blueprint.
    
4.  In the **Content Browser**, open **`BP_DartLauncher`**.
    
5.  In its **Details** panel, in the **Projectile** section, set the Projectile Class to `BP_FoamDart`, then save and compile the Blueprint.  
    
    [![](https://dev.epicgames.com/community/api/documentation/image/a2dd1b0a-7963-46ff-b260-eaa2b2493713?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a2dd1b0a-7963-46ff-b260-eaa2b2493713?resizing_type=fit)
    
    If you don't see `BP_FoamDart` in the list, go to the Content Browser, select `BP_FoamDart`, then go back to the **Projectile Class** property and click **Use Selected Asset from Content Browser**.
    

It’s time for the big reveal. Save your assets and click **Play**. When the game begins, you can run to the dart launcher to pick it up. Pressing the left mouse button spawns a projectile from the muzzle of the dart launcher and bounces it around the level! These projectiles should disappear after five seconds and impart a small physics force on objects they collide with (including you!).

## Next Up

Congratulations! You’ve completed the First-Person Programmer Track tutorial and learned a lot along the way! 

You’ve implemented custom characters and movement, created pickups and data assets, and even made equippable tools with their own projectiles. You’ve got everything you need to take this project and turn it into something all your own. 

Here are a few suggestions:

-   Can you expand the player’s inventory with different types of items? What about stacks of items?
    
-   Can you combine pickups and projectiles to create pickupable ammo? How about implementing this ammo system in the dart launcher?
    
-   Can you develop the idea of consumables into equippable consumables? How about a health pack the player holds, or a ball they can pick up and throw?
    

## Complete Code

C++

FirstPersonProjectile.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "FirstPersonProjectile.generated.h"  class UProjectileMovementComponent; class USphereComponent;`

```

Expand codeCopy full snippet(54 lines long)

C++

FirstPersonProjectile.cpp

```code
`// Fill out your copyright notice in the Description page of Project Settings.   #include "FirstPersonProjectile.h" #include "GameFramework/ProjectileMovementComponent.h" #include "Components/SphereComponent.h"  // Sets default values AFirstPersonProjectile::AFirstPersonProjectile() {`

```

Expand codeCopy full snippet(74 lines long)

C++

AdventureCharacter.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "Camera/CameraComponent.h" #include "EnhancedInputComponent.h" #include "EnhancedInputSubsystems.h"  #include "GameFramework/Character.h" #include "InputActionValue.h"`

```

Expand codeCopy full snippet(113 lines long)

C++

AdventureCharacter.cpp

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "AdventureCharacter.h" #include "EquippableToolBase.h" #include "EquippableToolDefinition.h" #include "ItemDefinition.h" #include "InventoryComponent.h"  // Sets default values AAdventureCharacter::AAdventureCharacter()`

```

Expand codeCopy full snippet(272 lines long)

C++

DartLauncher.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "AdventureGame/EquippableToolBase.h" #include "AdventureGame/FirstPersonProjectile.h" #include "DartLauncher.generated.h"  class AFirstPersonProjectile;`

```

Expand codeCopy full snippet(33 lines long)

C++

DartLauncher.cpp

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "DartLauncher.h" #include "Kismet/KismetMathLibrary.h" #include "AdventureGame/AdventureCharacter.h"  void ADartLauncher::Use() {  	UWorld* const World = GetWorld();`

```

Expand codeCopy full snippet(55 lines long)