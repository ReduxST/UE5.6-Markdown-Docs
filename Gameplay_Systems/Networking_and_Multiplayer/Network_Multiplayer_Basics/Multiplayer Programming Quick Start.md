# Multiplayer Programming Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multiplayer-programming-quick-start-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/multiplayer-programming-quick-start-for-unreal-engine)  
**Processed:** 2025-06-14 16:37:37

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e779479c-5702-4026-b72d-9388f36fa11a/preview.png)

Developing gameplay for a multiplayer game requires you to implement **replication** in your game's **Actors**. You must also design functionality specific to the **server**, which acts as the host for the game session, or a **client**, which represents a player connecting to the session. This guide walks you through the process of creating some simple multiplayer gameplay, and you will learn the following:

-   How to add replication to a base Actor.
-   How to take advantage of **Movement Components** in a network game.
-   How to add replication to **variables**.
-   How to use **RepNotifies** when a variable changes.
-   How to use **Remote Procedure Calls (RPCs)** in C++.
-   How to check an Actor's **Network Role** in order to filter calls that are performed within a function.

The end result will be a third-person game where players can throw exploding projectiles at one another. The bulk of the work we do will be creating the projectile and adding a damage response to the Character.

Before you begin, it is highly recommend, that you review the essentials in the [Dedicated Servers](/documentation/en-us/unreal-engine/setting-up-dedicated-servers-in-unreal-engine) and [Networking Overview](/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine) pages. As a point of comparison for this guide, you can refer to the [First Person Shooter Tutorial](/documentation/en-us/unreal-engine/first-person-shooter-tutorial-in-unreal-engine), which does not introduce replication concepts.

## 1\. Essential Setup

1.  Open the **Editor** and create a **New Project**. Ensure that it has the following settings:
    
    -   Is a **C++ Project**
    -   Uses the **Third-Person Template**
    -   Includes **Starter Content**
    -   Targets **Desktop**
    
    Once you have applied these settings, name your project **ThirdPersonMP** and click the **Create** button to continue. The project's C++ files will be created, and the **Unreal Editor** will open **ThirdPersonExampleMap** automatically.
    
2.  Click the **ThirdPersonCharacter** standing in this scene and **Delete** it, then ensure, that there are two **Player Starts** are present in your map. These will handle spawning your players instead of the manually placed ThirdPersonCharacter, that the scene includes by default.
    
    ![Add PlayerStarts](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfc64570-c435-4e42-99c6-5f23283fb460/01_addplayerstarts.png)

The Pawns and Characters in most templates have replication enabled by default. In this example, ThirdPersonCharacter already has a **Character Movement Component**, that will automatically replicate movement.

For more information on how the Character Movement Component handles replication and how to expand on its functionality, you can refer to the [Character Movement Component](/documentation/en-us/unreal-engine/understanding-networked-movement-in-the-character-movement-component-for-unreal-engine) guide.

Cosmetic components like the Character's **Skeletal Mesh** and its **Animation Blueprint** are not replicated. However, variables that are relevant to gameplay and movement, like a Character's velocity, are replicated. The Animation Blueprint reads these variables as they are updated. In this way, copies of each client's characters will update their visuals. The process is performed in such a way that they are consistent with accurate updating of gameplay variables Likewise, the [**Gameplay Framework**](/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine) automatically handles spawning Characters at Player Starts and assigning **Player Controllers** to them.

If you start a server with this project and have a client join it, you would already have a functioning multiplayer game. However, players would only be able to move and jump with their avatar. Therefore, you will create some additional multiplayer gameplay.

## 2\. Replicating the Player's Health with RepNotifies

Players need a health value, so that you can cause damage to them during gameplay. That value needs to replicate and all clients have synchronized information about each player's health. You need to provide feedback to a player, when they take damage. This section will demonstrate how it is possible to use a RepNotify to synchronize all essential updates to a variable without relying on RPCs.

Just a quick reminder, that 'Role' has been replaced with 'GetLocalRole()' and 'GetRemoteRole()' respectively. You'll notice some sections below, that might have previously used 'Role' so just be mindful of the change.

1.  Open `ThirdPersonMPCharacter.h`. Add the following Properties under `protected`:
    
2.  Open `ThirdPersonMPCharacter.h`. Add the following Properties under `protected`:
    
    ThirdPersonMPCharacter.h
    ```
         `protected:           /** The player's maximum health. This is the highest value of their health can be. This value is a value of the player's health, which starts at when spawned.*/          UPROPERTY(EditDefaultsOnly, Category = "Health")          float MaxHealth;           /** The player's current health. When reduced to 0, they are considered dead.*/          UPROPERTY(ReplicatedUsing = OnRep_CurrentHealth)          float CurrentHealth;           /** RepNotify for changes made to current health.*/          UFUNCTION()          void OnRep_CurrentHealth();`
    
    Copy full snippet
    ```
    protected: /\*\* The player's maximum health. This is the highest value of their health can be. This value is a value of the player's health, which starts at when spawned.\*/ UPROPERTY(EditDefaultsOnly, Category = "Health") float MaxHealth; /\*\* The player's current health. When reduced to 0, they are considered dead.\*/ UPROPERTY(ReplicatedUsing = OnRep\_CurrentHealth) float CurrentHealth; /\*\* RepNotify for changes made to current health.\*/ UFUNCTION() void OnRep\_CurrentHealth();

You need strictly control how the player's health is changed, therefore these health values have the following constraints:

-   `MaxHealth` does not replicate and is only editable in defaults. This value is pre-computed for all players, and will never change.
-   `CurrentHealth` replicates, but is not editable or accessible anywhere in Blueprint.
-   Both `MaxHealth` and `CurrentHealth` are `protected`, which prevents them from being accessed from external C++ classes. They can only be modified within `AThirdPersonMPCharacter` or other classes derived from it.

This minimizes the risk of causing unwanted changes to a player's `CurrentHealth` or `MaxHealth` during live gameplay. You will provide other public functions for getting and modifying these values in a later step.

The `Replicated` specifier enables the copy of an Actor on the server to replicate the value of a variable to all connected clients any time it changes. `ReplicatedUsing` does the same thing, but enables you to set a **RepNotify** function. This function will be triggered, when a client successfully receives the replicated data. You will use `OnRep_CurrentHealth` to perform updates to each client based on changes to this variable.

1.  Open `ThirdPersonMPCharacter.cpp`. Add the following `#include` statements at the top, underneath the line that reads `#include "GameFramework/SpringArmComponent.h"`:
    
    ThirdPersonMPCharacter.cpp
    ```
         `#include "Net/UnrealNetwork.h"      #include "Engine/Engine.h"`
    
    Copy full snippet
    ```
    #include "Net/UnrealNetwork.h" #include "Engine/Engine.h"
    
    These provide required functionality for variable replication, as well as access to the `AddOnscreenDebugMessage` function in `GEngine`. You will use it to output messages to the screen.
    
2.  In `ThirdPersonMPCharacter.cpp`, add the following code at the bottom of the `AThirdPersonMPCharacter` constructor :
    
    ThirdPersonMPCharacter.cpp
    ```
         `//Initialize the player's Health      MaxHealth = 100.0f;      CurrentHealth = MaxHealth;`
    
    Copy full snippet
    ```
    //Initialize the player's Health MaxHealth = 100.0f; CurrentHealth = MaxHealth;
    
    These will initialize the player's health. Any time a new copy of this Character is created, its current health will be set to its maximum health value.
    
3.  In `ThirdPersonMPCharacter.h`, add the following public function declaration just after the `AThirdPersonMPCharacter` constructor:
    
    ThirdPersonMPCharacter.h
    ```
         `/** Property replication */      void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;`
    
    Copy full snippet
    ```
    /\*\* Property replication \*/ void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;
4.  In `ThirdPersonMPCharacter.cpp`, add the following implementation for this function:
    
    ThirdPersonMPCharacter.cpp
    ```
        `//////////////////////////////////////////////////////////////////////////     // Replicated Properties      void AThirdPersonMPCharacter::GetLifetimeReplicatedProps(TArray <FLifetimeProperty>& OutLifetimeProps) const     {         Super::GetLifetimeReplicatedProps(OutLifetimeProps);          //Replicate current health.         DOREPLIFETIME(AThirdPersonMPCharacter, CurrentHealth);     }`
    
    Copy full snippet
    ```
    ////////////////////////////////////////////////////////////////////////// // Replicated Properties void AThirdPersonMPCharacter::GetLifetimeReplicatedProps(TArray <FLifetimeProperty>& OutLifetimeProps) const { Super::GetLifetimeReplicatedProps(OutLifetimeProps); //Replicate current health. DOREPLIFETIME(AThirdPersonMPCharacter, CurrentHealth); }
    
    The `GetLifetimeReplicatedProps` function is responsible for replicating any properties you designate with the `Replicated` specifier, and enables you to configure how a property will replicate. Here you are using the most basic implementation for `CurrentHealth`. If at any time you add more properties that need to be replicated, you must add them to this function as well.
    
    You must call the `Super` version of `GetLifetimeReplicatedProps`, or inherited properties from your Actor's parent class will not replicate, even if the parent class designates them as being replicated.
    
5.  In `ThirdPersonMPCharacter.h`, add the following function declaration under `Protected`:
    
    ThirdPersonMPCharacter.h
    ```
         `protected:          /** Response to health being updated. Called on the server immediately after modification, and on clients in response to a RepNotify*/          void OnHealthUpdate();`
    
    Copy full snippet
    ```
    protected: /\*\* Response to health being updated. Called on the server immediately after modification, and on clients in response to a RepNotify\*/ void OnHealthUpdate();
6.  In `ThirdPersonMPCharacter.cpp`, add the following implementation:
    
    ThirdPersonMPCharacter.cpp
    ```
         `void AThirdPersonMPCharacter::OnHealthUpdate()      {          //Client-specific functionality          if (IsLocallyControlled())          {              FString healthMessage = FString::Printf(TEXT("You now have %f health remaining."), CurrentHealth);              GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Blue, healthMessage);               if (CurrentHealth <= 0)              {                  FString deathMessage = FString::Printf(TEXT("You have been killed."));                  GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, deathMessage);              }          }           //Server-specific functionality          if (GetLocalRole() == ROLE_Authority)          {              FString healthMessage = FString::Printf(TEXT("%s now has %f health remaining."), *GetFName().ToString(), CurrentHealth);              GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Blue, healthMessage);          }           //Functions that occur on all machines.          /*              Any special functionality that should occur as a result of damage or death should be placed here.          */      }`
    
    Copy full snippet
    ```
    void AThirdPersonMPCharacter::OnHealthUpdate() { //Client-specific functionality if (IsLocallyControlled()) { FString healthMessage = FString::Printf(TEXT("You now have %f health remaining."), CurrentHealth); GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Blue, healthMessage); if (CurrentHealth <= 0) { FString deathMessage = FString::Printf(TEXT("You have been killed.")); GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, deathMessage); } } //Server-specific functionality if (GetLocalRole() == ROLE\_Authority) { FString healthMessage = FString::Printf(TEXT("%s now has %f health remaining."), \*GetFName().ToString(), CurrentHealth); GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Blue, healthMessage); } //Functions that occur on all machines. /\* Any special functionality that should occur as a result of damage or death should be placed here. \*/ }
    
    You will be using this function to perform updates in response to changes to the player's `CurrentHealth`. Currently its functionality is limited to onscreen debug messages, but additional functionality could be added. For example, an `OnDeath` function, that is called on all machines in order to trigger a death animation. Note, that `OnHealthUpdate` is not replicated, and you will need to manually call it on all devices.
    
7.  In `ThirdPersonMPCharacter.cpp`, add the following implementation for `OnRep_CurrentHealth`:
    
    ThirdPersonMPCharacter.cpp
    ```
         `void AThirdPersonMPCharacter::OnRep_CurrentHealth()      {          OnHealthUpdate();      }`
    
    Copy full snippet
    ```
    void AThirdPersonMPCharacter::OnRep\_CurrentHealth() { OnHealthUpdate(); }
    
    Variables replicate any time their value changes rather than constantly replicating, and `RepNotifies` run any time the client successfully receives a replicated value for a variable. Therefore, any time you change the player's `CurrentHealth` on the server, you would expect `OnRep_CurrentHealth` to run on each connected client. This makes `OnRep_CurrentHealth` the ideal place to call `OnHealthUpdate` on clients' machines.
    

## 3\. Making the Player Respond to Damage

Now, that you have implemented the player's health, you need to provide a means for modifying the player's health from outside of this class.

1.  In `ThirdPersonMPCharacter.h`, add the following function declarations under `Public`:
    
    ThirdPersonMPCharacter.h
    ```
         `public:          /** Getter for Max Health.*/          UFUNCTION(BlueprintPure, Category="Health")          FORCEINLINE float GetMaxHealth() const { return MaxHealth; }           /** Getter for Current Health.*/          UFUNCTION(BlueprintPure, Category="Health")          FORCEINLINE float GetCurrentHealth() const { return CurrentHealth; }           /** Setter for Current Health. Clamps the value between 0 and MaxHealth and calls OnHealthUpdate. Should only be called on the server.*/          UFUNCTION(BlueprintCallable, Category="Health")          void SetCurrentHealth(float healthValue);           /** Event for taking damage. Overridden from APawn.*/          UFUNCTION(BlueprintCallable, Category = "Health")          float TakeDamage( float DamageTaken, struct FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser ) override;`
    
    Copy full snippet
    ```
    public: /\*\* Getter for Max Health.\*/ UFUNCTION(BlueprintPure, Category="Health") FORCEINLINE float GetMaxHealth() const { return MaxHealth; } /\*\* Getter for Current Health.\*/ UFUNCTION(BlueprintPure, Category="Health") FORCEINLINE float GetCurrentHealth() const { return CurrentHealth; } /\*\* Setter for Current Health. Clamps the value between 0 and MaxHealth and calls OnHealthUpdate. Should only be called on the server.\*/ UFUNCTION(BlueprintCallable, Category="Health") void SetCurrentHealth(float healthValue); /\*\* Event for taking damage. Overridden from APawn.\*/ UFUNCTION(BlueprintCallable, Category = "Health") float TakeDamage( float DamageTaken, struct FDamageEvent const& DamageEvent, AController\* EventInstigator, AActor\* DamageCauser ) override;
    
    The `GetMaxHealth` and `GetCurrentHealth` functions provide getters, that can access the player's health values from outside of `AThirdPersonMPCharacter`, both in C++ and in Blueprint. As `const` functions they provide a safe means of getting these values without allowing them to be modified. You are also declaring functions for setting the player's health and taking damage.
    
2.  In `ThirdPersonMPCharacter.cpp`, add the following implementation for `SetCurrentHealth`:
    
    ThirdPersonMPCharacter.cpp
    ```
         `void AThirdPersonMPCharacter::SetCurrentHealth(float healthValue)      {          if (GetLocalRole() == ROLE_Authority)          {              CurrentHealth = FMath::Clamp(healthValue, 0.f, MaxHealth);              OnHealthUpdate();          }      }`
    
    Copy full snippet
    ```
    void AThirdPersonMPCharacter::SetCurrentHealth(float healthValue) { if (GetLocalRole() == ROLE\_Authority) { CurrentHealth = FMath::Clamp(healthValue, 0.f, MaxHealth); OnHealthUpdate(); } }
    
    `SetCurrentHealth` provides a controlled means of modifying the player's `CurrentHealth` from outside of `AThirdPersonMPCharacter`. It is not a replicated function, but by checking that the Network Role of the Actor is `ROLE_Authority`, you restrict this function to execute only if it is called on the hosted game server. It clamps `CurrentHealth` to values between 0 and the player's `MaxHealth`, making it impossible to set `CurrentHealth` to an invalid value. It also calls `OnHealthUpdate` to ensure, that the server and clients both have parallel calls to this function. This is necessary, because the server will not receive the RepNotify.
    
    While "setter" functions like this are not necessary for every variable, they are preferable for sensitive gameplay variables, that change frequently during play, especially if they can be modified by many different sources. This is a best-practice for single-player and multiplayer games alike, as it makes live changes to these variables more consistent, easier to debug, and easier to extend with new functionality.
    
3.  In `ThirdPersonMPCharacter.cpp`, add the following implementation for `TakeDamage`:
    
    ThirdPersonMPCharacter.cpp
    ```
         `float AThirdPersonMPCharacter::TakeDamage(float DamageTaken, struct FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser)      {          float damageApplied = CurrentHealth - DamageTaken;          SetCurrentHealth(damageApplied);          return damageApplied;      }`
    
    Copy full snippet
    ```
    float AThirdPersonMPCharacter::TakeDamage(float DamageTaken, struct FDamageEvent const& DamageEvent, AController\* EventInstigator, AActor\* DamageCauser) { float damageApplied = CurrentHealth - DamageTaken; SetCurrentHealth(damageApplied); return damageApplied; }
    
    The built-in functions for applying damage to Actors call the basic `TakeDamage` function for that Actor. In this case you implement a simple health deduction using `SetCurrentHealth`.
    

If you have followed this section so far, the following should now be the flow for applying damage to an Actor:

-   An external Actor or function calls `CauseDamage` on your Character, which in turn calls its `TakeDamage` function.
-   `TakeDamage` calls `SetCurrentHealth` to change the player's Current Health value on the server.
-   `SetCurrentHealth` calls `OnHealthUpdate` on the server, causing any functionality, that happens in response to changes in the player's health, to execute.
-   `CurrentHealth` replicates to all connected clients' copies of the Character.
-   When each client receives a new `CurrentHealth` value from the server, they call `OnRep_CurrentHealth`.
-   `OnRep_CurrentHealth` calls `OnHealthUpdate`, ensuring that each client responds the same way to the new `CurrentHealth` value.

This implementation has two main advantages. First, it condenses the workflow for adding new functionality around two key functions, namely `SetCurrentHealth` and `OnHealthUpdate`, which makes maintaining and expanding the code easier for the future. Second, since this implementation does not use any Server, Client, or NetMulticast RPCs, it condenses the amount of information being sent across the network, depending only on the replication of `CurrentHealth` to trigger all essential changes. Since `CurrentHealth` would need to replicate regardless of what other functions you implement, this is the most efficient possible model for replicating health changes.

## 4\. Creating a Projectile with Replication

1.  Inside the Unreal Editor, create a **new C++ class** using either the **Tools** menu or the **Content Browser**.
    
    ![Create New Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a2d14a5-e259-418a-9094-d1ee5101b64d/02_createnewcppclass.png)
2.  In the **Choose Parent Class** menu, choose **Actor** as the Parent Class and click **Next**.
    
    Click image for full view.
    
3.  In the **Name Your New Actor** menu, name your class **ThirdPersonMPProjectile** and click **Create Class**.
    
    Click image for full view.
    
4.  Open `ThirdPersonMPProjectile.h` and add the following code inside the class definition, under `public`:
    
    ThirdPersonMPProjectile.h
    ```
         `public:          // Sphere component used to test collision.          UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Components")          class USphereComponent* SphereComponent;           // Static Mesh used to provide a visual representation of the object.          UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Components")          class UStaticMeshComponent* StaticMesh;           // Movement component for handling projectile movement.          UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Components")          class UProjectileMovementComponent* ProjectileMovementComponent;           // Particle used when the projectile impacts against another object and explodes.          UPROPERTY(EditAnywhere, Category = "Effects")          class UParticleSystem* ExplosionEffect;           //The damage type and damage that will be done by this projectile          UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Damage")          TSubclassOf<class UDamageType> DamageType;           //The damage dealt by this projectile.          UPROPERTY(EditAnywhere, BlueprintReadOnly, Category="Damage")          float Damage;`
    
    Copy full snippet
    ```
    public: // Sphere component used to test collision. UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Components") class USphereComponent\* SphereComponent; // Static Mesh used to provide a visual representation of the object. UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Components") class UStaticMeshComponent\* StaticMesh; // Movement component for handling projectile movement. UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Components") class UProjectileMovementComponent\* ProjectileMovementComponent; // Particle used when the projectile impacts against another object and explodes. UPROPERTY(EditAnywhere, Category = "Effects") class UParticleSystem\* ExplosionEffect; //The damage type and damage that will be done by this projectile UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Damage") TSubclassOf<class UDamageType> DamageType; //The damage dealt by this projectile. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category="Damage") float Damage;
    
    You need precede each of the types in these declarations with the `class` keyword. This makes each of them a forward declaration of their own classes in addition to being variable declarations, which ensures that their classes will be recognized within the header file. You will be adding `#include`s for them in the CPP file during the next step.
    
    The properties you are declaring will provide you with the following:
    
    -   A **Static Mesh Component** to act as a visual representation of the Projectile.
    -   A **Sphere Component** to check for collisions.
    -   A **Projectile Movement Component** to move the Projectile.
    -   A **Particle System** reference that you are going to use to spawn an explosion effect in a later step.
    -   A **Damage Type** for use in damage events.
    -   A float value for **Damage** to denote how much health should be subtracted, when a Character is hit by this Projectile.
    
    However, none of these are defined yet.
    
    Like the Character Movement Component, the Projectile Movement Component automatically handles replication, when it moves the Actor that it belongs to, provided that the Actor has `bReplicates` set to `True`.
    
5.  Open `ThirdPersonMPProjectile.cpp`, and add the following code to the `#include` statements at the top of the file, underneath the line `#include "ThirdPersonMPProjectile.h"`:
    
    ThirdPersonMPProjectile.cpp
    ```
         `#include "Components/SphereComponent.h"      #include "Components/StaticMeshComponent.h"      #include "GameFramework/ProjectileMovementComponent.h"      #include "GameFramework/DamageType.h"      #include "Particles/ParticleSystem.h"      #include "Kismet/GameplayStatics.h"      #include "UObject/ConstructorHelpers.h"`
    
    Copy full snippet
    ```
    #include "Components/SphereComponent.h" #include "Components/StaticMeshComponent.h" #include "GameFramework/ProjectileMovementComponent.h" #include "GameFramework/DamageType.h" #include "Particles/ParticleSystem.h" #include "Kismet/GameplayStatics.h" #include "UObject/ConstructorHelpers.h"
    
    You will need use each of these throughout this walkthrough. The first four are the components you are using, while `GamePlayStatics.h` will give you access to basic gameplay functions, and `ConstructorHelpers.h` will give you access to some useful Constructor functions for setting up our components.
    
6.  Add the following code inside of the `AThirdPersonMPProjectile` constructor:
    
    ThirdPersonMPProjectile.cpp
    ```
         `bReplicates = true;`
    
    Copy full snippet
    ```
    bReplicates = true;
    
    The `bReplicates` variable tells the game that this Actor should replicate. By default, the Actor would only exist locally on the machine that spawns it. With `bReplicates` set to `True`, as long as an authoritative copy of the Actor exists on the server, it will try to replicate the Actor to all connected clients.
    
7.  Add the following code inside of the `AThirdPersonMPProjectile` constructor:
    
    ThirdPersonMPProjectile.cpp
    ```
         `//Definition for the SphereComponent that will serve as the Root component for the projectile and its collision.      SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent"));      SphereComponent->InitSphereRadius(37.5f);      SphereComponent->SetCollisionProfileName(TEXT("BlockAllDynamic"));      RootComponent = SphereComponent;`
    
    Copy full snippet
    ```
    //Definition for the SphereComponent that will serve as the Root component for the projectile and its collision. SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); SphereComponent->InitSphereRadius(37.5f); SphereComponent->SetCollisionProfileName(TEXT("BlockAllDynamic")); RootComponent = SphereComponent;
    
    This will define the SphereComponent when the object is constructed, giving your Projectile collision.
    
8.  Add the following code inside of the `AThirdPersonMPProjectile` constructor:
    
    ThirdPersonMPProjectile.cpp
    ```
         `//Definition for the Mesh that will serve as your visual representation.      static ConstructorHelpers::FObjectFinder<UStaticMesh> DefaultMesh(TEXT("/Game/StarterContent/Shapes/Shape_Sphere.Shape_Sphere"));      StaticMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh"));      StaticMesh->SetupAttachment(RootComponent);       //Set the Static Mesh and its position/scale if you successfully found a mesh asset to use.      if (DefaultMesh.Succeeded())      {          StaticMesh->SetStaticMesh(DefaultMesh.Object);          StaticMesh->SetRelativeLocation(FVector(0.0f, 0.0f, -37.5f));          StaticMesh->SetRelativeScale3D(FVector(0.75f, 0.75f, 0.75f));      }`
    
    Copy full snippet
    ```
    //Definition for the Mesh that will serve as your visual representation. static ConstructorHelpers::FObjectFinder<UStaticMesh> DefaultMesh(TEXT("/Game/StarterContent/Shapes/Shape\_Sphere.Shape\_Sphere")); StaticMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh")); StaticMesh->SetupAttachment(RootComponent); //Set the Static Mesh and its position/scale if you successfully found a mesh asset to use. if (DefaultMesh.Succeeded()) { StaticMesh->SetStaticMesh(DefaultMesh.Object); StaticMesh->SetRelativeLocation(FVector(0.0f, 0.0f, -37.5f)); StaticMesh->SetRelativeScale3D(FVector(0.75f, 0.75f, 0.75f)); }
    
    This will define the StaticMeshComponent that you are using as a visual representation. It will automatically try to find the **Shape\_Sphere** mesh inside of **StarterContent** and fill it in. The sphere will also be scaled so as to align with your SphereComponent in size.
    
9.  Add the following code inside of the `AThirdPersonMPProjectile` constructor:
    
    ThirdPersonMPProjectile.cpp
    ```
         `static ConstructorHelpers::FObjectFinder<UParticleSystem> DefaultExplosionEffect(TEXT("/Game/StarterContent/Particles/P_Explosion.P_Explosion"));      if (DefaultExplosionEffect.Succeeded())      {          ExplosionEffect = DefaultExplosionEffect.Object;      }`
    
    Copy full snippet
    ```
    static ConstructorHelpers::FObjectFinder<UParticleSystem> DefaultExplosionEffect(TEXT("/Game/StarterContent/Particles/P\_Explosion.P\_Explosion")); if (DefaultExplosionEffect.Succeeded()) { ExplosionEffect = DefaultExplosionEffect.Object; }
    
    This will set the asset reference for your `ExplosionEffect` to be the **P\_Explosion** asset inside of StarterContent.
    
10.  Add the following code inside of the `AThirdPersonMPProjectile` constructor:
    
    ThirdPersonMPProjectile.cpp
    ```
         `//Definition for the Projectile Movement Component.      ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovement"));      ProjectileMovementComponent->SetUpdatedComponent(SphereComponent);      ProjectileMovementComponent->InitialSpeed = 1500.0f;      ProjectileMovementComponent->MaxSpeed = 1500.0f;      ProjectileMovementComponent->bRotationFollowsVelocity = true;      ProjectileMovementComponent->ProjectileGravityScale = 0.0f;`
    
    Copy full snippet
    ```
    //Definition for the Projectile Movement Component. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovement")); ProjectileMovementComponent->SetUpdatedComponent(SphereComponent); ProjectileMovementComponent->InitialSpeed = 1500.0f; ProjectileMovementComponent->MaxSpeed = 1500.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->ProjectileGravityScale = 0.0f;
    
    This will define the Projectile Movement Component for your Projectile. This Component is replicated, and any movement that it performs on the server will be reproduced on clients.
    
11.  Add the following code inside of the `AThirdPersonMPProjectile` constructor:
    
    ThirdPersonMPProjectile.cpp
    ```
         `DamageType = UDamageType::StaticClass();      Damage = 10.0f;`
    
    Copy full snippet
    ```
    DamageType = UDamageType::StaticClass(); Damage = 10.0f;
    
    These will initialize both the amount of Damage that the Projectile will deal to an Actor as well as the Damage Type that will be used in the damage event. Here you are initializing with the base `UDamageType`, as you have not yet defined any new Damage Types.
    

## 5\. Making the Projectile Cause Damage

If you have been following along thus far, then it is possible for you to spawn the projectile on the server, and it will appear and move on all clients. However, if it hits a wall or a blocking object, it will stop. You need it to apply damage to players, and you need to show an explosion effect to all of the connected Clients in the session.

1.  In `ThirdPersonMPProjectile.h`, add the following code under `Protected`:
    
    ThirdPersonMPProjectile.h
    ```
         `protected:          virtual void Destroyed() override;`
    
    Copy full snippet
    ```
    protected: virtual void Destroyed() override;
2.  In `ThirdPersonMPProjectile.cpp`, add the following implementation for this function:
    
    ThirdPersonMPProjectile.cpp
    ```
         `void AThirdPersonMPProjectile::Destroyed()      {          FVector spawnLocation = GetActorLocation();          UGameplayStatics::SpawnEmitterAtLocation(this, ExplosionEffect, spawnLocation, FRotator::ZeroRotator, true, EPSCPoolMethod::AutoRelease);      }`
    
    Copy full snippet
    ```
    void AThirdPersonMPProjectile::Destroyed() { FVector spawnLocation = GetActorLocation(); UGameplayStatics::SpawnEmitterAtLocation(this, ExplosionEffect, spawnLocation, FRotator::ZeroRotator, true, EPSCPoolMethod::AutoRelease); }
    
    The `Destroyed` function is called any time an Actor is destroyed. Particle emitters themselves do not normally replicate, but since Actor destruction does replicate, you destroy this projectile on the server. This function will be called on each connected client, when they destroy their own copies of it. As a result, all players will see the explosion effect, when the projectile is destroyed.
    
3.  In `ThirdPersonMPProjectile.h`, add the following code under `Protected`:
    
    ThirdPersonMPProjectile.h
    ```
         `UFUNCTION(Category="Projectile")      void OnProjectileImpact(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit);`
    
    Copy full snippet
    ```
    UFUNCTION(Category="Projectile") void OnProjectileImpact(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, FVector NormalImpulse, const FHitResult& Hit);
4.  In `ThirdPersonMPProjectile.cpp`, add the following implementations for this function:
    
    ThirdPersonMPProjectile.cpp
    ```
         `void AThirdPersonMPProjectile::OnProjectileImpact(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit)      {          if ( OtherActor )          {              UGameplayStatics::ApplyPointDamage(OtherActor, Damage, NormalImpulse, Hit, GetInstigator()->Controller, this, DamageType);          }           Destroy();      }`
    
    Copy full snippet
    ```
    void AThirdPersonMPProjectile::OnProjectileImpact(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, FVector NormalImpulse, const FHitResult& Hit) { if ( OtherActor ) { UGameplayStatics::ApplyPointDamage(OtherActor, Damage, NormalImpulse, Hit, GetInstigator()->Controller, this, DamageType); } Destroy(); }
    
    This is the function, that you are going to call when the Projectile impacts with an object. If the object it impacts with is a valid Actor, it will call the `ApplyPointDamage` function to damage it at the point, where the collision takes place. Meanwhile, any collision regardless of the impacted surface will destroy this Actor, causing the explosion effect to appear.
    
5.  In `ThirdPersonMPProjectile.cpp`, add the following code to the `AThirdPersonMPProjectile` constructor, underneath the line that reads `RootComponent = SphereComponent`:
    
    ThirdPersonMPProjectile.cpp
    ```
         `//Registering the Projectile Impact function on a Hit event.      if (GetLocalRole() == ROLE_Authority)      {          SphereComponent->OnComponentHit.AddDynamic(this, &AThirdPersonMPProjectile::OnProjectileImpact);      }`
    
    Copy full snippet
    ```
    //Registering the Projectile Impact function on a Hit event. if (GetLocalRole() == ROLE\_Authority) { SphereComponent->OnComponentHit.AddDynamic(this, &AThirdPersonMPProjectile::OnProjectileImpact); }
    
    This will register the `OnProjectileImpact` function with the `OnComponentHit` event on the Sphere Component, which acts as the projectile's primary collision component. To make especially sure, that only the server runs this gameplay logic, you check for `GetLocalRole() == ROLE_Authority` before registering `OnProjectileImpact`.
    

## 6\. Shooting the Projectile

1.  Open the **Unreal Editor**, then click the **Edit** drop-down menu at the top of the screen, and open your **Project Settings**.
    
    ![Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e497c641-7592-4d3f-b70f-fff4e22a1b92/05_projectsettings.png)
2.  In the **Engine** section, click on **Input** to open up your project's Input Settings. Unfold the **Bindings** section and add a new entry to it. Name it "**Fire**", and select the **Left Mouse Button** as the key this Action is bound to.
    
    Click image for full view.
    
3.  In `ThirdPersonMPCharacter.cpp`, add the following `#include`, underneath the line that reads `#include "Engine/Engine.h"`:
    
    ThirdPersonMPCharacter.cpp
    ```
         `#include "ThirdPersonMPProjectile.h"`
    
    Copy full snippet
    ```
    #include "ThirdPersonMPProjectile.h"
    
    This will enable your Character class to recognize the projectile's type and spawn it.
    
4.  In `ThirdPersonMPCharacter.h`, add the following code under `protected`:
    
    ThirdPersonMPCharacter.h
    ```
         `protected:          UPROPERTY(EditDefaultsOnly, Category="Gameplay|Projectile")          TSubclassOf<class AThirdPersonMPProjectile> ProjectileClass;           /** Delay between shots in seconds. Used to control fire rate for your test projectile, but also to prevent an overflow of server functions from binding SpawnProjectile directly to input.*/          UPROPERTY(EditDefaultsOnly, Category="Gameplay")          float FireRate;           /** If true, you are in the process of firing projectiles. */          bool bIsFiringWeapon;           /** Function for beginning weapon fire.*/          UFUNCTION(BlueprintCallable, Category="Gameplay")          void StartFire();           /** Function for ending weapon fire. Once this is called, the player can use StartFire again.*/          UFUNCTION(BlueprintCallable, Category = "Gameplay")          void StopFire();           /** Server function for spawning projectiles.*/          UFUNCTION(Server, Reliable)          void HandleFire();           /** A timer handle used for providing the fire rate delay in-between spawns.*/          FTimerHandle FiringTimer;`
    
    Copy full snippet
    ```
    protected: UPROPERTY(EditDefaultsOnly, Category="Gameplay|Projectile") TSubclassOf<class AThirdPersonMPProjectile> ProjectileClass; /\*\* Delay between shots in seconds. Used to control fire rate for your test projectile, but also to prevent an overflow of server functions from binding SpawnProjectile directly to input.\*/ UPROPERTY(EditDefaultsOnly, Category="Gameplay") float FireRate; /\*\* If true, you are in the process of firing projectiles. \*/ bool bIsFiringWeapon; /\*\* Function for beginning weapon fire.\*/ UFUNCTION(BlueprintCallable, Category="Gameplay") void StartFire(); /\*\* Function for ending weapon fire. Once this is called, the player can use StartFire again.\*/ UFUNCTION(BlueprintCallable, Category = "Gameplay") void StopFire(); /\*\* Server function for spawning projectiles.\*/ UFUNCTION(Server, Reliable) void HandleFire(); /\*\* A timer handle used for providing the fire rate delay in-between spawns.\*/ FTimerHandle FiringTimer;
    
    These are the variables and functions you will be using to fire your projectiles. `HandleFire` is the only RPC you will implement in this tutorial, and it will be responsible for spawning projectiles on the server. Because it has the `Server` specifier, any attempt to call it on a client will result in the call being directed over the network to the authoritative Character on the server instead.
    
    Because `HandleFire` has the `Reliable` specifier as well, it is placed into a queue for reliable RPCs whenever it gets called, and it is removed from the queue, when the server successfully receives it. This guarnatees that the server will definitely receive this function call. However, the queue for reliable RPCs can overflow if too many RPCs are placed into it at once without removing them, and if it does then it will force the user to disconnect. Therefore, you need to be cautious in how often you allow players to call this function.
    
5.  In `ThirdPersonMPCharacter.cpp`, add the following code to the bottom of the `AThirdPersonMPCharacter` constructor:
    
    ThirdPersonMPCharacter.cpp
    ```
         `//Initialize projectile class      ProjectileClass = AThirdPersonMPProjectile::StaticClass();      //Initialize fire rate      FireRate = 0.25f;      bIsFiringWeapon = false;`
    
    Copy full snippet
    ```
    //Initialize projectile class ProjectileClass = AThirdPersonMPProjectile::StaticClass(); //Initialize fire rate FireRate = 0.25f; bIsFiringWeapon = false;
    
    These will initialize the variables necessary to handle firing the projectile.
    
6.  In `ThirdPersonMPCharacter.cpp`, add the following implementations:
    
    ThirdPersonMPCharacter.cpp
    ```
         `void AThirdPersonMPCharacter::StartFire()      {          if (!bIsFiringWeapon)          {              bIsFiringWeapon = true;              UWorld* World = GetWorld();              World->GetTimerManager().SetTimer(FiringTimer, this, &AThirdPersonMPCharacter::StopFire, FireRate, false);              HandleFire();          }      }       void AThirdPersonMPCharacter::StopFire()      {          bIsFiringWeapon = false;      }       void AThirdPersonMPCharacter::HandleFire_Implementation()      {          FVector spawnLocation = GetActorLocation() + ( GetActorRotation().Vector()  * 100.0f ) + (GetActorUpVector() * 50.0f);          FRotator spawnRotation = GetActorRotation();           FActorSpawnParameters spawnParameters;          spawnParameters.Instigator = GetInstigator();          spawnParameters.Owner = this;           AThirdPersonMPProjectile* spawnedProjectile = GetWorld()->SpawnActor<AThirdPersonMPProjectile>(spawnLocation, spawnRotation, spawnParameters);      }`
    
    Copy full snippet
    ```
    void AThirdPersonMPCharacter::StartFire() { if (!bIsFiringWeapon) { bIsFiringWeapon = true; UWorld\* World = GetWorld(); World->GetTimerManager().SetTimer(FiringTimer, this, &AThirdPersonMPCharacter::StopFire, FireRate, false); HandleFire(); } } void AThirdPersonMPCharacter::StopFire() { bIsFiringWeapon = false; } void AThirdPersonMPCharacter::HandleFire\_Implementation() { FVector spawnLocation = GetActorLocation() + ( GetActorRotation().Vector() \* 100.0f ) + (GetActorUpVector() \* 50.0f); FRotator spawnRotation = GetActorRotation(); FActorSpawnParameters spawnParameters; spawnParameters.Instigator = GetInstigator(); spawnParameters.Owner = this; AThirdPersonMPProjectile\* spawnedProjectile = GetWorld()->SpawnActor<AThirdPersonMPProjectile>(spawnLocation, spawnRotation, spawnParameters); }
    
    `StartFire` is the function, that players call on their local machine in order to initiate the firing process, and it restricts how often the user is allowed to call `HandleFire` based on the following criteria:
    
    -   The user cannot fire a projectile if they are already in the middle of firing. This is designated with `bFiringWeapon`, which is set to `true` when `StartFire` is called.
    -   `bFiringWeapon` is only set to `false` when `StopFire` is called.
    -   `StopFire` is called when a timer with a length of `FireRate` finishes.
    
    This means that when the user fires a projectile, they must wait a number of seconds equal to `FireRate` before they can fire again. This will function consistently regarldess of what kind of input `StartFire` is bound to. For example, if the user binds the "Fire" command to a scroll wheel or similarly inappropriate input, or if they mash the button repeatedly, this function will still execute at an acceptable interval of time and not overflow the user's queue for reliable functions with calls to `HandleFire`.
    
    Because `HandleFire` is a Server RPC, its implementation in the CPP file must have the suffix `_Implementation` added to the function name. Our implementation here uses the Character's Control Rotation to get the direction that the camera is facing, then spawn the projectile facing in that direction, enabling the player to aim. The projectile's Projectile Movement Component then handles moving it in that direction.
    
7.  In `ThirdPersonMPCharacter.cpp`, add the following at the bottom of the function `SetupPlayerInputComponent`:
    
    ThirdPersonMPCharacter.cpp
    ```
         `// Handle firing projectiles      PlayerInputComponent->BindAction("Fire", IE_Pressed, this, &AThirdPersonMPCharacter::StartFire);`
    
    Copy full snippet
    ```
    // Handle firing projectiles PlayerInputComponent->BindAction("Fire", IE\_Pressed, this, &AThirdPersonMPCharacter::StartFire);
    
    This binds `StartFire` to the **Fire** Input Action you created in the first step of this section, enabling the user to activate it.
    

## 7\. Test Your Game

1.  Open your Project in the Editor. Click the **Edit** drop-down menu, and open **Editor Preferences**.
    
    ![Open Level Editor/Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a609916-d187-4737-b17e-a469aa5177b5/07_editorpreference.png)
2.  Navigate to the **Level Editor** section and click the **Play** menu. Find the **Multiplayer Options** and change the **Play Net Mode** to **Play As Listen Server**. Also, set **Play Number Of Clients** to **2**.
    
    Click image for full view.
    
3.  Press the **Play** button. The main **Play in Editor (PIE)** window will start a Multiplayer Session as the Server, and a second PIE window will open and connect as the Client.
    

## Final Result

Click image for full view.

Both players in your game should be able to see each other moving, and they should also be able to shoot the custom projectile at each other. When one player is hit by the custom projectile, the explosion particle should appear for both players, and the player taking the hit will receive a "hit" message telling them how much damage they took and their current health, while all other players in the session should not see anything. If a player's health is reduced to 0, they should see a message informing them that they have been killed.

Now that you have completed this walkthrough, you should have a grasp on the basics of building multiplayer functionality in C++, including an overview of variable and component replication, how to work with Network Roles, and when it is appropriate to use RPCs. With this information you shlould be able to build your own multiplayer games within Unreal's Server-Client model.

## On Your Own

To continue expanding your skills with Network Multiplayer programming, try to do the following:

-   Expand the Projectile's OnHit functionality to create additional effects, when the Projectile hits a target, like creating a Sphere Trace to simulate an explosion radius.
-   Extend ThirdPersonMPProjectile and experiment with its ProjectileMovement Component to create new variations with different behaviors.
-   Expand the TakeDamage function in ThirdPersonMPCharacter to kill the player's pawn and make them respawn.
-   Add a HUD to the local PlayerController and have it display replicated information or respond to Client functions.
-   Use DamageTypes to create personalized messages when a player is killed.
-   Explore the use of Game Mode, Player State, and Game State to create a complete set of rules for moderating a match with player stats and a scoreboard.

## Code Samples

ThirdPersonMPProjectile.h
```
	`// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "ThirdPersonMPProjectile.generated.h"  	UCLASS() 	class THIRDPERSONMP_API AThirdPersonMPProjectile : public AActor 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this actor's properties 		AThirdPersonMPProjectile();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick(float DeltaTime) override;  	public: 		// Sphere component used to test collision. 		UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components") 		class USphereComponent* SphereComponent;  		// Static Mesh used to provide a visual representation of the object. 		UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components") 		class UStaticMeshComponent* StaticMesh;  		// Movement component for handling projectile movement. 		UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components") 		class UProjectileMovementComponent* ProjectileMovementComponent;  		// Particle used when the projectile impacts against another object and explodes. 		UPROPERTY(EditAnywhere, Category = "Effects") 		class UParticleSystem* ExplosionEffect;  		//The damage type and damage that will be done by this projectile 		UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Damage") 		TSubclassOf<class UDamageType> DamageType;  		//The damage dealt by this projectile. 		UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Damage") 		float Damage;  	protected:  		virtual void Destroyed() override;  		UFUNCTION(Category = "Projectile") 		void OnProjectileImpact(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit);  	};`

Copy full snippet
```
// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "ThirdPersonMPProjectile.generated.h" UCLASS() class THIRDPERSONMP\_API AThirdPersonMPProjectile : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AThirdPersonMPProjectile(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick(float DeltaTime) override; public: // Sphere component used to test collision. UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components") class USphereComponent\* SphereComponent; // Static Mesh used to provide a visual representation of the object. UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components") class UStaticMeshComponent\* StaticMesh; // Movement component for handling projectile movement. UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components") class UProjectileMovementComponent\* ProjectileMovementComponent; // Particle used when the projectile impacts against another object and explodes. UPROPERTY(EditAnywhere, Category = "Effects") class UParticleSystem\* ExplosionEffect; //The damage type and damage that will be done by this projectile UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Damage") TSubclassOf<class UDamageType> DamageType; //The damage dealt by this projectile. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Damage") float Damage; protected: virtual void Destroyed() override; UFUNCTION(Category = "Projectile") void OnProjectileImpact(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, FVector NormalImpulse, const FHitResult& Hit); }; ThirdPersonMPProjectile.cpp
```
	`// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#include "ThirdPersonMPProjectile.h" 	#include "Components/SphereComponent.h" 	#include "Components/StaticMeshComponent.h" 	#include "GameFramework/ProjectileMovementComponent.h" 	#include "GameFramework/DamageType.h" 	#include "Particles/ParticleSystem.h" 	#include "Kismet/GameplayStatics.h" 	#include "UObject/ConstructorHelpers.h"  	// Sets default values 	AThirdPersonMPProjectile::AThirdPersonMPProjectile() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		bReplicates = true;  		//Definition for the SphereComponent that will serve as the Root component for the projectile and its collision. 		SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); 		SphereComponent->InitSphereRadius(37.5f); 		SphereComponent->SetCollisionProfileName(TEXT("BlockAllDynamic")); 		RootComponent = SphereComponent;  		//Registering the Projectile Impact function on a Hit event. 		if (GetLocalRole() == ROLE_Authority) 		{ 			SphereComponent->OnComponentHit.AddDynamic(this, &AThirdPersonMPProjectile::OnProjectileImpact); 		}  		//Definition for the Mesh that will serve as your visual representation. 		static ConstructorHelpers::FObjectFinder<UStaticMesh> DefaultMesh(TEXT("/Game/StarterContent/Shapes/Shape_Sphere.Shape_Sphere")); 		StaticMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh")); 		StaticMesh->SetupAttachment(RootComponent);  		//Set the Static Mesh and its position/scale if you successfully found a mesh asset to use. 		if (DefaultMesh.Succeeded()) 		{ 			StaticMesh->SetStaticMesh(DefaultMesh.Object); 			StaticMesh->SetRelativeLocation(FVector(0.0f, 0.0f, -37.5f)); 			StaticMesh->SetRelativeScale3D(FVector(0.75f, 0.75f, 0.75f)); 		}  		static ConstructorHelpers::FObjectFinder<UParticleSystem> DefaultExplosionEffect(TEXT("/Game/StarterContent/Particles/P_Explosion.P_Explosion")); 		if (DefaultExplosionEffect.Succeeded()) 		{ 			ExplosionEffect = DefaultExplosionEffect.Object; 		}  		//Definition for the Projectile Movement Component. 		ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovement")); 		ProjectileMovementComponent->SetUpdatedComponent(SphereComponent); 		ProjectileMovementComponent->InitialSpeed = 1500.0f; 		ProjectileMovementComponent->MaxSpeed = 1500.0f; 		ProjectileMovementComponent->bRotationFollowsVelocity = true; 		ProjectileMovementComponent->ProjectileGravityScale = 0.0f;  		DamageType = UDamageType::StaticClass(); 		Damage = 10.0f; 	}  	// Called when the game starts or when spawned 	void AThirdPersonMPProjectile::BeginPlay() 	{ 		Super::BeginPlay(); 	}  	// Called every frame 	void AThirdPersonMPProjectile::Tick(float DeltaTime) 	{ 		Super::Tick(DeltaTime); 	}  	void AThirdPersonMPProjectile::Destroyed() 	{ 		FVector spawnLocation = GetActorLocation(); 		UGameplayStatics::SpawnEmitterAtLocation(this, ExplosionEffect, spawnLocation, FRotator::ZeroRotator, true, EPSCPoolMethod::AutoRelease); 	}  	void AThirdPersonMPProjectile::OnProjectileImpact(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit) 	{ 		if (OtherActor) 		{ 			UGameplayStatics::ApplyPointDamage(OtherActor, Damage, NormalImpulse, Hit, GetInstigator()->Controller, this, DamageType); 		} 		Destroy(); 	}`

Copy full snippet
```
// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved. #include "ThirdPersonMPProjectile.h" #include "Components/SphereComponent.h" #include "Components/StaticMeshComponent.h" #include "GameFramework/ProjectileMovementComponent.h" #include "GameFramework/DamageType.h" #include "Particles/ParticleSystem.h" #include "Kismet/GameplayStatics.h" #include "UObject/ConstructorHelpers.h" // Sets default values AThirdPersonMPProjectile::AThirdPersonMPProjectile() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; bReplicates = true; //Definition for the SphereComponent that will serve as the Root component for the projectile and its collision. SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); SphereComponent->InitSphereRadius(37.5f); SphereComponent->SetCollisionProfileName(TEXT("BlockAllDynamic")); RootComponent = SphereComponent; //Registering the Projectile Impact function on a Hit event. if (GetLocalRole() == ROLE\_Authority) { SphereComponent->OnComponentHit.AddDynamic(this, &AThirdPersonMPProjectile::OnProjectileImpact); } //Definition for the Mesh that will serve as your visual representation. static ConstructorHelpers::FObjectFinder<UStaticMesh> DefaultMesh(TEXT("/Game/StarterContent/Shapes/Shape\_Sphere.Shape\_Sphere")); StaticMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh")); StaticMesh->SetupAttachment(RootComponent); //Set the Static Mesh and its position/scale if you successfully found a mesh asset to use. if (DefaultMesh.Succeeded()) { StaticMesh->SetStaticMesh(DefaultMesh.Object); StaticMesh->SetRelativeLocation(FVector(0.0f, 0.0f, -37.5f)); StaticMesh->SetRelativeScale3D(FVector(0.75f, 0.75f, 0.75f)); } static ConstructorHelpers::FObjectFinder<UParticleSystem> DefaultExplosionEffect(TEXT("/Game/StarterContent/Particles/P\_Explosion.P\_Explosion")); if (DefaultExplosionEffect.Succeeded()) { ExplosionEffect = DefaultExplosionEffect.Object; } //Definition for the Projectile Movement Component. ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileMovement")); ProjectileMovementComponent->SetUpdatedComponent(SphereComponent); ProjectileMovementComponent->InitialSpeed = 1500.0f; ProjectileMovementComponent->MaxSpeed = 1500.0f; ProjectileMovementComponent->bRotationFollowsVelocity = true; ProjectileMovementComponent->ProjectileGravityScale = 0.0f; DamageType = UDamageType::StaticClass(); Damage = 10.0f; } // Called when the game starts or when spawned void AThirdPersonMPProjectile::BeginPlay() { Super::BeginPlay(); } // Called every frame void AThirdPersonMPProjectile::Tick(float DeltaTime) { Super::Tick(DeltaTime); } void AThirdPersonMPProjectile::Destroyed() { FVector spawnLocation = GetActorLocation(); UGameplayStatics::SpawnEmitterAtLocation(this, ExplosionEffect, spawnLocation, FRotator::ZeroRotator, true, EPSCPoolMethod::AutoRelease); } void AThirdPersonMPProjectile::OnProjectileImpact(UPrimitiveComponent\* HitComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, FVector NormalImpulse, const FHitResult& Hit) { if (OtherActor) { UGameplayStatics::ApplyPointDamage(OtherActor, Damage, NormalImpulse, Hit, GetInstigator()->Controller, this, DamageType); } Destroy(); } ThirdPersonMPCharacter.h
```
	`// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Character.h" 	#include "ThirdPersonMPCharacter.generated.h"  	UCLASS(config=Game) 	class AThirdPersonMPCharacter : public ACharacter 	{ 		GENERATED_BODY()  		/** Camera boom positioning the camera behind the character */ 		UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Camera, meta = (AllowPrivateAccess = "true")) 		class USpringArmComponent* CameraBoom;  		/** Follow camera */ 		UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Camera, meta = (AllowPrivateAccess = "true")) 		class UCameraComponent* FollowCamera;  	public:  		AThirdPersonMPCharacter();  		/** Property replication */ 		void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;  		/** Base turn rate, in deg/sec. Other scaling may affect final turn rate. */ 		UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category=Input) 		float TurnRateGamepad;  	protected:  		/** Called for forwards/backward input */ 		void MoveForward(float Value);  		/** Called for side to side input */ 		void MoveRight(float Value);  		/** 		* Called via input to turn at a given rate. 		* @param Rate	This is a normalized rate, i.e. 1.0 means 100% of desired turn rate 		*/ 		void TurnAtRate(float Rate);  		/** 		* Called via input to turn look up/down at a given rate. 		* @param Rate	This is a normalized rate, i.e. 1.0 means 100% of desired turn rate 		*/ 		void LookUpAtRate(float Rate);  		/** Handler for when a touch input begins. */ 		void TouchStarted(ETouchIndex::Type FingerIndex, FVector Location);  		/** Handler for when a touch input stops. */ 		void TouchStopped(ETouchIndex::Type FingerIndex, FVector Location);  		// APawn interface 		virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override; 		// End of APawn interface  	public:  		/** Returns CameraBoom subobject **/ 		FORCEINLINE class USpringArmComponent* GetCameraBoom() const { return CameraBoom; }  		/** Returns FollowCamera subobject **/ 		FORCEINLINE class UCameraComponent* GetFollowCamera() const { return FollowCamera; }  	protected:  		/** The player's maximum health. This is the highest value of their health can be. This value is a value of the player's health, which starts at when spawned.*/ 		UPROPERTY(EditDefaultsOnly, Category = "Health") 		float MaxHealth;  		/** The player's current health. When reduced to 0, they are considered dead.*/ 		UPROPERTY(ReplicatedUsing = OnRep_CurrentHealth) 		float CurrentHealth;  		/** RepNotify for changes made to current health.*/ 		UFUNCTION() 		void OnRep_CurrentHealth();  		/** Response to health being updated. Called on the server immediately after modification, and on clients in response to a RepNotify*/ 		void OnHealthUpdate();  	public:  		/** Getter for Max Health.*/ 		UFUNCTION(BlueprintPure, Category = "Health") 		FORCEINLINE float GetMaxHealth() const { return MaxHealth; }  		/** Getter for Current Health.*/ 		UFUNCTION(BlueprintPure, Category = "Health") 		FORCEINLINE float GetCurrentHealth() const { return CurrentHealth; }  		/** Setter for Current Health. Clamps the value between 0 and MaxHealth and calls OnHealthUpdate. Should only be called on the server.*/ 		UFUNCTION(BlueprintCallable, Category = "Health") 		void SetCurrentHealth(float healthValue);  		/** Event for taking damage. Overridden from APawn.*/ 		UFUNCTION(BlueprintCallable, Category = "Health") 		float TakeDamage(float DamageTaken, struct FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser) override;  	protected:  		UPROPERTY(EditDefaultsOnly, Category = "Gameplay|Projectile") 		TSubclassOf<class AThirdPersonMPProjectile> ProjectileClass;  		/** Delay between shots in seconds. Used to control fire rate for your test projectile, but also to prevent an overflow of server functions from binding SpawnProjectile directly to input.*/ 		UPROPERTY(EditDefaultsOnly, Category = "Gameplay") 		float FireRate;  		/** If true, you are in the process of firing projectiles. */ 		bool bIsFiringWeapon;  		/** Function for beginning weapon fire.*/ 		UFUNCTION(BlueprintCallable, Category = "Gameplay") 		void StartFire();  		/** Function for ending weapon fire. Once this is called, the player can use StartFire again.*/ 		UFUNCTION(BlueprintCallable, Category = "Gameplay") 		void StopFire();  		/** Server function for spawning projectiles.*/ 		UFUNCTION(Server, Reliable) 		void HandleFire();  		/** A timer handle used for providing the fire rate delay in-between spawns.*/ 		FTimerHandle FiringTimer; 	};`

Copy full snippet
```
// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Character.h" #include "ThirdPersonMPCharacter.generated.h" UCLASS(config=Game) class AThirdPersonMPCharacter : public ACharacter { GENERATED\_BODY() /\*\* Camera boom positioning the camera behind the character \*/ UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Camera, meta = (AllowPrivateAccess = "true")) class USpringArmComponent\* CameraBoom; /\*\* Follow camera \*/ UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Camera, meta = (AllowPrivateAccess = "true")) class UCameraComponent\* FollowCamera; public: AThirdPersonMPCharacter(); /\*\* Property replication \*/ void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override; /\*\* Base turn rate, in deg/sec. Other scaling may affect final turn rate. \*/ UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category=Input) float TurnRateGamepad; protected: /\*\* Called for forwards/backward input \*/ void MoveForward(float Value); /\*\* Called for side to side input \*/ void MoveRight(float Value); /\*\* \* Called via input to turn at a given rate. \* @param Rate This is a normalized rate, i.e. 1.0 means 100% of desired turn rate \*/ void TurnAtRate(float Rate); /\*\* \* Called via input to turn look up/down at a given rate. \* @param Rate This is a normalized rate, i.e. 1.0 means 100% of desired turn rate \*/ void LookUpAtRate(float Rate); /\*\* Handler for when a touch input begins. \*/ void TouchStarted(ETouchIndex::Type FingerIndex, FVector Location); /\*\* Handler for when a touch input stops. \*/ void TouchStopped(ETouchIndex::Type FingerIndex, FVector Location); // APawn interface virtual void SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) override; // End of APawn interface public: /\*\* Returns CameraBoom subobject \*\*/ FORCEINLINE class USpringArmComponent\* GetCameraBoom() const { return CameraBoom; } /\*\* Returns FollowCamera subobject \*\*/ FORCEINLINE class UCameraComponent\* GetFollowCamera() const { return FollowCamera; } protected: /\*\* The player's maximum health. This is the highest value of their health can be. This value is a value of the player's health, which starts at when spawned.\*/ UPROPERTY(EditDefaultsOnly, Category = "Health") float MaxHealth; /\*\* The player's current health. When reduced to 0, they are considered dead.\*/ UPROPERTY(ReplicatedUsing = OnRep\_CurrentHealth) float CurrentHealth; /\*\* RepNotify for changes made to current health.\*/ UFUNCTION() void OnRep\_CurrentHealth(); /\*\* Response to health being updated. Called on the server immediately after modification, and on clients in response to a RepNotify\*/ void OnHealthUpdate(); public: /\*\* Getter for Max Health.\*/ UFUNCTION(BlueprintPure, Category = "Health") FORCEINLINE float GetMaxHealth() const { return MaxHealth; } /\*\* Getter for Current Health.\*/ UFUNCTION(BlueprintPure, Category = "Health") FORCEINLINE float GetCurrentHealth() const { return CurrentHealth; } /\*\* Setter for Current Health. Clamps the value between 0 and MaxHealth and calls OnHealthUpdate. Should only be called on the server.\*/ UFUNCTION(BlueprintCallable, Category = "Health") void SetCurrentHealth(float healthValue); /\*\* Event for taking damage. Overridden from APawn.\*/ UFUNCTION(BlueprintCallable, Category = "Health") float TakeDamage(float DamageTaken, struct FDamageEvent const& DamageEvent, AController\* EventInstigator, AActor\* DamageCauser) override; protected: UPROPERTY(EditDefaultsOnly, Category = "Gameplay|Projectile") TSubclassOf<class AThirdPersonMPProjectile> ProjectileClass; /\*\* Delay between shots in seconds. Used to control fire rate for your test projectile, but also to prevent an overflow of server functions from binding SpawnProjectile directly to input.\*/ UPROPERTY(EditDefaultsOnly, Category = "Gameplay") float FireRate; /\*\* If true, you are in the process of firing projectiles. \*/ bool bIsFiringWeapon; /\*\* Function for beginning weapon fire.\*/ UFUNCTION(BlueprintCallable, Category = "Gameplay") void StartFire(); /\*\* Function for ending weapon fire. Once this is called, the player can use StartFire again.\*/ UFUNCTION(BlueprintCallable, Category = "Gameplay") void StopFire(); /\*\* Server function for spawning projectiles.\*/ UFUNCTION(Server, Reliable) void HandleFire(); /\*\* A timer handle used for providing the fire rate delay in-between spawns.\*/ FTimerHandle FiringTimer; }; ThirdPersonMPCharacter.cpp
```
	`// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#include "ThirdPersonMPCharacter.h" 	#include "Camera/CameraComponent.h" 	#include "Components/CapsuleComponent.h" 	#include "Components/InputComponent.h" 	#include "GameFramework/CharacterMovementComponent.h" 	#include "GameFramework/Controller.h" 	#include "GameFramework/SpringArmComponent.h" 	#include "Net/UnrealNetwork.h" 	#include "Engine/Engine.h" 	#include "ThirdPersonMPProjectile.h"  	////////////////////////////////////////////////////////////////////////// 	// AThirdPersonMPCharacter  	AThirdPersonMPCharacter::AThirdPersonMPCharacter() 	{ 		// Set size for collision capsule 		GetCapsuleComponent()->InitCapsuleSize(42.f, 96.0f);  		// set our turn rate for input 		TurnRateGamepad = 50.f;  		// Don't rotate when the controller rotates. Let that just affect the camera. 		bUseControllerRotationPitch = false; 		bUseControllerRotationYaw = false; 		bUseControllerRotationRoll = false;  		// Configure character movement 		GetCharacterMovement()->bOrientRotationToMovement = true; // Character moves in the direction of input... 		GetCharacterMovement()->RotationRate = FRotator(0.0f, 500.0f, 0.0f); // ...at this rotation rate  		// Note: For faster iteration times these variables, and many more, can be tweaked in the Character Blueprint 		// instead of recompiling to adjust them 		GetCharacterMovement()->JumpZVelocity = 700.f; 		GetCharacterMovement()->AirControl = 0.35f; 		GetCharacterMovement()->MaxWalkSpeed = 500.f; 		GetCharacterMovement()->MinAnalogWalkSpeed = 20.f; 		GetCharacterMovement()->BrakingDecelerationWalking = 2000.f;  		// Create a camera boom (pulls in towards the player if there is a collision) 		CameraBoom = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraBoom")); 		CameraBoom->SetupAttachment(RootComponent); 		CameraBoom->TargetArmLength = 400.0f; // The camera follows at this distance behind the character 		CameraBoom->bUsePawnControlRotation = true; // Rotate the arm based on the controller  		// Create a follow camera 		FollowCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("FollowCamera")); 		FollowCamera->SetupAttachment(CameraBoom, USpringArmComponent::SocketName); // Attach the camera to the end of the boom and let the boom adjust to match the controller orientation 		FollowCamera->bUsePawnControlRotation = false; // Camera does not rotate relative to arm  		// Note: The skeletal mesh and anim blueprint references on the Mesh component (inherited from Character) 		// are set in the derived blueprint asset named ThirdPersonCharacter (to avoid direct content references in C++)  		//Initialize the player's Health 		MaxHealth = 100.0f; 		CurrentHealth = MaxHealth;  		//Initialize projectile class 		ProjectileClass = AThirdPersonMPProjectile::StaticClass(); 		//Initialize fire rate 		FireRate = 0.25f; 		bIsFiringWeapon = false; 	}  	////////////////////////////////////////////////////////////////////////// 	// Input  	void AThirdPersonMPCharacter::SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) 	{ 		// Set up gameplay key bindings 		check(PlayerInputComponent); 		PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &ACharacter::Jump); 		PlayerInputComponent->BindAction("Jump", IE_Released, this, &ACharacter::StopJumping);  		PlayerInputComponent->BindAxis("Move Forward / Backward", this, &AThirdPersonMPCharacter::MoveForward); 		PlayerInputComponent->BindAxis("Move Right / Left", this, &AThirdPersonMPCharacter::MoveRight);  		// We have 2 versions of the rotation bindings to handle different kinds of devices differently 		// "turn" handles devices that provide an absolute delta, such as a mouse. 		// "turnrate" is for devices that we choose to treat as a rate of change, such as an analog joystick 		PlayerInputComponent->BindAxis("Turn Right / Left Mouse", this, &APawn::AddControllerYawInput); 		PlayerInputComponent->BindAxis("Turn Right / Left Gamepad", this, &AThirdPersonMPCharacter::TurnAtRate); 		PlayerInputComponent->BindAxis("Look Up / Down Mouse", this, &APawn::AddControllerPitchInput); 		PlayerInputComponent->BindAxis("Look Up / Down Gamepad", this, &AThirdPersonMPCharacter::LookUpAtRate);  		// handle touch devices 		PlayerInputComponent->BindTouch(IE_Pressed, this, &AThirdPersonMPCharacter::TouchStarted); 		PlayerInputComponent->BindTouch(IE_Released, this, &AThirdPersonMPCharacter::TouchStopped);  		// Handle firing projectiles 		PlayerInputComponent->BindAction("Fire", IE_Pressed, this, &AThirdPersonMPCharacter::StartFire); 	}  	void AThirdPersonMPCharacter::TouchStarted(ETouchIndex::Type FingerIndex, FVector Location) 	{ 		Jump(); 	}  	void AThirdPersonMPCharacter::TouchStopped(ETouchIndex::Type FingerIndex, FVector Location) 	{ 		StopJumping(); 	}  	void AThirdPersonMPCharacter::TurnAtRate(float Rate) 	{ 		// calculate delta for this frame from the rate information 		AddControllerYawInput(Rate * TurnRateGamepad * GetWorld()->GetDeltaSeconds()); 	}  	void AThirdPersonMPCharacter::LookUpAtRate(float Rate) 	{ 		// calculate delta for this frame from the rate information 		AddControllerPitchInput(Rate * TurnRateGamepad * GetWorld()->GetDeltaSeconds()); 	}  	void AThirdPersonMPCharacter::MoveForward(float Value) 	{ 		if ((Controller != nullptr) && (Value != 0.0f)) 		{ 			// find out which way is forward 			const FRotator Rotation = Controller->GetControlRotation(); 			const FRotator YawRotation(0, Rotation.Yaw, 0);  			// get forward vector 			const FVector Direction = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::X); 			AddMovementInput(Direction, Value); 		} 	}  	void AThirdPersonMPCharacter::MoveRight(float Value) 	{ 		if ( (Controller != nullptr) && (Value != 0.0f) ) 		{ 			// find out which way is right 			const FRotator Rotation = Controller->GetControlRotation(); 			const FRotator YawRotation(0, Rotation.Yaw, 0);  			// get right vector 			const FVector Direction = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::Y); 			// add movement in that direction 			AddMovementInput(Direction, Value); 		} 	}  	////////////////////////////////////////////////////////////////////////// 	// Replicated Properties  	void AThirdPersonMPCharacter::GetLifetimeReplicatedProps(TArray <FLifetimeProperty>& OutLifetimeProps) const 	{ 		Super::GetLifetimeReplicatedProps(OutLifetimeProps);  		//Replicate current health. 		DOREPLIFETIME(AThirdPersonMPCharacter, CurrentHealth); 	}  	void AThirdPersonMPCharacter::OnHealthUpdate() 	{ 		//Client-specific functionality 		if (IsLocallyControlled()) 		{ 			FString healthMessage = FString::Printf(TEXT("You now have %f health remaining."), CurrentHealth); 			GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Blue, healthMessage);  			if (CurrentHealth <= 0) 			{ 				FString deathMessage = FString::Printf(TEXT("You have been killed.")); 				GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, deathMessage); 			} 		}  		//Server-specific functionality 		if (GetLocalRole() == ROLE_Authority) 		{ 			FString healthMessage = FString::Printf(TEXT("%s now has %f health remaining."), *GetFName().ToString(), CurrentHealth); 			GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Blue, healthMessage); 		}  		//Functions that occur on all machines. 		/* 			Any special functionality that should occur as a result of damage or death should be placed here. 		*/ 	}  	void AThirdPersonMPCharacter::OnRep_CurrentHealth() 	{ 		OnHealthUpdate(); 	}  	void AThirdPersonMPCharacter::SetCurrentHealth(float healthValue) 	{ 		if (GetLocalRole() == ROLE_Authority) 		{ 			CurrentHealth = FMath::Clamp(healthValue, 0.f, MaxHealth); 			OnHealthUpdate(); 		} 	}  	float AThirdPersonMPCharacter::TakeDamage(float DamageTaken, struct FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser) 	{ 		float damageApplied = CurrentHealth - DamageTaken; 		SetCurrentHealth(damageApplied); 		return damageApplied; 	}  	void AThirdPersonMPCharacter::StartFire() 	{ 		if (!bIsFiringWeapon) 		{ 			bIsFiringWeapon = true; 			UWorld* World = GetWorld(); 			World->GetTimerManager().SetTimer(FiringTimer, this, &AThirdPersonMPCharacter::StopFire, FireRate, false); 			HandleFire(); 		} 	}  	void AThirdPersonMPCharacter::StopFire() 	{ 		bIsFiringWeapon = false; 	}  	void AThirdPersonMPCharacter::HandleFire_Implementation() 	{ 		FVector spawnLocation = GetActorLocation() + (GetActorRotation().Vector() * 100.0f) + (GetActorUpVector() * 50.0f); 		FRotator spawnRotation = GetActorRotation();  		FActorSpawnParameters spawnParameters; 		spawnParameters.Instigator = GetInstigator(); 		spawnParameters.Owner = this;  		AThirdPersonMPProjectile* spawnedProjectile = GetWorld()->SpawnActor<AThirdPersonMPProjectile>(spawnLocation, spawnRotation, spawnParameters); 	}`
Copy full snippet
```
// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved. #include "ThirdPersonMPCharacter.h" #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h" #include "Components/InputComponent.h" #include "GameFramework/CharacterMovementComponent.h" #include "GameFramework/Controller.h" #include "GameFramework/SpringArmComponent.h" #include "Net/UnrealNetwork.h" #include "Engine/Engine.h" #include "ThirdPersonMPProjectile.h" ////////////////////////////////////////////////////////////////////////// // AThirdPersonMPCharacter AThirdPersonMPCharacter::AThirdPersonMPCharacter() { // Set size for collision capsule GetCapsuleComponent()->InitCapsuleSize(42.f, 96.0f); // set our turn rate for input TurnRateGamepad = 50.f; // Don't rotate when the controller rotates. Let that just affect the camera. bUseControllerRotationPitch = false; bUseControllerRotationYaw = false; bUseControllerRotationRoll = false; // Configure character movement GetCharacterMovement()->bOrientRotationToMovement = true; // Character moves in the direction of input... GetCharacterMovement()->RotationRate = FRotator(0.0f, 500.0f, 0.0f); // ...at this rotation rate // Note: For faster iteration times these variables, and many more, can be tweaked in the Character Blueprint // instead of recompiling to adjust them GetCharacterMovement()->JumpZVelocity = 700.f; GetCharacterMovement()->AirControl = 0.35f; GetCharacterMovement()->MaxWalkSpeed = 500.f; GetCharacterMovement()->MinAnalogWalkSpeed = 20.f; GetCharacterMovement()->BrakingDecelerationWalking = 2000.f; // Create a camera boom (pulls in towards the player if there is a collision) CameraBoom = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraBoom")); CameraBoom->SetupAttachment(RootComponent); CameraBoom->TargetArmLength = 400.0f; // The camera follows at this distance behind the character CameraBoom->bUsePawnControlRotation = true; // Rotate the arm based on the controller // Create a follow camera FollowCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("FollowCamera")); FollowCamera->SetupAttachment(CameraBoom, USpringArmComponent::SocketName); // Attach the camera to the end of the boom and let the boom adjust to match the controller orientation FollowCamera->bUsePawnControlRotation = false; // Camera does not rotate relative to arm // Note: The skeletal mesh and anim blueprint references on the Mesh component (inherited from Character) // are set in the derived blueprint asset named ThirdPersonCharacter (to avoid direct content references in C++) //Initialize the player's Health MaxHealth = 100.0f; CurrentHealth = MaxHealth; //Initialize projectile class ProjectileClass = AThirdPersonMPProjectile::StaticClass(); //Initialize fire rate FireRate = 0.25f; bIsFiringWeapon = false; } ////////////////////////////////////////////////////////////////////////// // Input void AThirdPersonMPCharacter::SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) { // Set up gameplay key bindings check(PlayerInputComponent); PlayerInputComponent->BindAction("Jump", IE\_Pressed, this, &ACharacter::Jump); PlayerInputComponent->BindAction("Jump", IE\_Released, this, &ACharacter::StopJumping); PlayerInputComponent->BindAxis("Move Forward / Backward", this, &AThirdPersonMPCharacter::MoveForward); PlayerInputComponent->BindAxis("Move Right / Left", this, &AThirdPersonMPCharacter::MoveRight); // We have 2 versions of the rotation bindings to handle different kinds of devices differently // "turn" handles devices that provide an absolute delta, such as a mouse. // "turnrate" is for devices that we choose to treat as a rate of change, such as an analog joystick PlayerInputComponent->BindAxis("Turn Right / Left Mouse", this, &APawn::AddControllerYawInput); PlayerInputComponent->BindAxis("Turn Right / Left Gamepad", this, &AThirdPersonMPCharacter::TurnAtRate); PlayerInputComponent->BindAxis("Look Up / Down Mouse", this, &APawn::AddControllerPitchInput); PlayerInputComponent->BindAxis("Look Up / Down Gamepad", this, &AThirdPersonMPCharacter::LookUpAtRate); // handle touch devices PlayerInputComponent->BindTouch(IE\_Pressed, this, &AThirdPersonMPCharacter::TouchStarted); PlayerInputComponent->BindTouch(IE\_Released, this, &AThirdPersonMPCharacter::TouchStopped); // Handle firing projectiles PlayerInputComponent->BindAction("Fire", IE\_Pressed, this, &AThirdPersonMPCharacter::StartFire); } void AThirdPersonMPCharacter::TouchStarted(ETouchIndex::Type FingerIndex, FVector Location) { Jump(); } void AThirdPersonMPCharacter::TouchStopped(ETouchIndex::Type FingerIndex, FVector Location) { StopJumping(); } void AThirdPersonMPCharacter::TurnAtRate(float Rate) { // calculate delta for this frame from the rate information AddControllerYawInput(Rate \* TurnRateGamepad \* GetWorld()->GetDeltaSeconds()); } void AThirdPersonMPCharacter::LookUpAtRate(float Rate) { // calculate delta for this frame from the rate information AddControllerPitchInput(Rate \* TurnRateGamepad \* GetWorld()->GetDeltaSeconds()); } void AThirdPersonMPCharacter::MoveForward(float Value) { if ((Controller != nullptr) && (Value != 0.0f)) { // find out which way is forward const FRotator Rotation = Controller->GetControlRotation(); const FRotator YawRotation(0, Rotation.Yaw, 0); // get forward vector const FVector Direction = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::X); AddMovementInput(Direction, Value); } } void AThirdPersonMPCharacter::MoveRight(float Value) { if ( (Controller != nullptr) && (Value != 0.0f) ) { // find out which way is right const FRotator Rotation = Controller->GetControlRotation(); const FRotator YawRotation(0, Rotation.Yaw, 0); // get right vector const FVector Direction = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::Y); // add movement in that direction AddMovementInput(Direction, Value); } } ////////////////////////////////////////////////////////////////////////// // Replicated Properties void AThirdPersonMPCharacter::GetLifetimeReplicatedProps(TArray <FLifetimeProperty>& OutLifetimeProps) const { Super::GetLifetimeReplicatedProps(OutLifetimeProps); //Replicate current health. DOREPLIFETIME(AThirdPersonMPCharacter, CurrentHealth); } void AThirdPersonMPCharacter::OnHealthUpdate() { //Client-specific functionality if (IsLocallyControlled()) { FString healthMessage = FString::Printf(TEXT("You now have %f health remaining."), CurrentHealth); GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Blue, healthMessage); if (CurrentHealth <= 0) { FString deathMessage = FString::Printf(TEXT("You have been killed.")); GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, deathMessage); } } //Server-specific functionality if (GetLocalRole() == ROLE\_Authority) { FString healthMessage = FString::Printf(TEXT("%s now has %f health remaining."), \*GetFName().ToString(), CurrentHealth); GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Blue, healthMessage); } //Functions that occur on all machines. /\* Any special functionality that should occur as a result of damage or death should be placed here. \*/ } void AThirdPersonMPCharacter::OnRep\_CurrentHealth() { OnHealthUpdate(); } void AThirdPersonMPCharacter::SetCurrentHealth(float healthValue) { if (GetLocalRole() == ROLE\_Authority) { CurrentHealth = FMath::Clamp(healthValue, 0.f, MaxHealth); OnHealthUpdate(); } } float AThirdPersonMPCharacter::TakeDamage(float DamageTaken, struct FDamageEvent const& DamageEvent, AController\* EventInstigator, AActor\* DamageCauser) { float damageApplied = CurrentHealth - DamageTaken; SetCurrentHealth(damageApplied); return damageApplied; } void AThirdPersonMPCharacter::StartFire() { if (!bIsFiringWeapon) { bIsFiringWeapon = true; UWorld\* World = GetWorld(); World->GetTimerManager().SetTimer(FiringTimer, this, &AThirdPersonMPCharacter::StopFire, FireRate, false); HandleFire(); } } void AThirdPersonMPCharacter::StopFire() { bIsFiringWeapon = false; } void AThirdPersonMPCharacter::HandleFire\_Implementation() { FVector spawnLocation = GetActorLocation() + (GetActorRotation().Vector() \* 100.0f) + (GetActorUpVector() \* 50.0f); FRotator spawnRotation = GetActorRotation(); FActorSpawnParameters spawnParameters; spawnParameters.Instigator = GetInstigator(); spawnParameters.Owner = this; AThirdPersonMPProjectile\* spawnedProjectile = GetWorld()->SpawnActor<AThirdPersonMPProjectile>(spawnLocation, spawnRotation, spawnParameters); }