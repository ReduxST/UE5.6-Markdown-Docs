# Create a Respawning Pickup Item

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/create-a-respawning-pickup-item-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/create-a-respawning-pickup-item-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:39

---

## Before You Begin

Ensure you’ve completed the following objectives in the previous section, [Manage Items and Data](https://dev.epicgames.com/documentation/en-us/unreal-engine/manage-item-and-data-in-an-unreal-engine-game):

-   Set up an Item Data Struct, `UDataAsset` class, a Consumable-type Data Asset instance named `DA_Pickup_001`, and a Data Table.
    

## Create a New Pickup Class

So far, you've learned to define and store an item's structure and data. In this section, you'll learn how to turn this data into an in-game "pickup", a concrete representation of table data that the player can interact with and gain an effect. A pickup could be an equippable gadget, a box that gives them materials, or a powerup that gives them a temporary boost.

To start setting up a pickup class with initial declarations, follow these steps: 

1.  In the Unreal Editor, go to **Tools** \> **New C++ Class**. Select **Actor** as the parent class and name the class `PickupBase`. Click **Create Class**.
    
2.  In Visual Studio, open `PickupBase.h` and add the following statements to the top of the file:
    
    -   `#include ”Components/SphereComponent.h”`. You’ll add a sphere component to the pickup to detect collisions between player and pickup.
        
    -   `#include ”AdventureCharacter.h”`. Add a reference to your first-person character class so you can check for overlaps between the pickup and characters of this class. (This tutorial uses `AdventureCharacter`.)
        
    -   A forward declaration for `UItemDefinition`. This is the associated Data Asset item that each pickup references.
        
    
    C++
    
    ```code
    `// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "Components/SphereComponent.h" #include "CoreMinimal.h" #include "AdventureCharacter.h" #include "GameFramework/Actor.h" #include "PickupBase.generated.h"`
    
    
    ```
    
    Expand codeCopy full snippet(11 lines long)
    
3.  In the `UCLASS()` macro above the `APickupBase` class definition, add the `BlueprintType` and `Blueprintable` specifiers to expose it as a base class for creating Blueprints.  
    
    C++
    
    `UCLASS(BlueprintType, Blueprintable) class ADVENTUREGAME_API APickupBase : public AActor {`
    
    UCLASS(BlueprintType, Blueprintable) class ADVENTUREGAME\_API APickupBase : public AActor {
    
    Copy full snippet(3 lines long)
    
4.  In `PickupBase.cpp`, add an `#include` for `ItemDefinition.h`.
    
    C++
    
    `// Copyright Epic Games, Inc. All Rights Reserved.  #include "PickupBase.h" #include "ItemDefinition.h"`
    
    // Copyright Epic Games, Inc. All Rights Reserved. #include &quot;PickupBase.h&quot; #include &quot;ItemDefinition.h&quot;
    
    Copy full snippet(4 lines long)
    

## Initialize the Pickup with Table Data

Your pickup is just a blank Actor, so when the game begins, you need to give it the data it needs to operate properly. The pickup should pull a row of values from the Data Table and save those values in an ItemDefinition Data Asset (the “reference item”). 

### Pull Data from a Data Table

In `PickupBase.h`, in the `public` section, declare a new void function `InitializePickup()`. You’ll use this function to initialize the pickup with values from the Data Table. 

C++

`// Initializes this pickup with values from the data table. void InitializePickup();`

// Initializes this pickup with values from the data table. void InitializePickup();

Copy full snippet(2 lines long)

To pull data from the table, the pickup Blueprint needs two properties: the Data Table asset and the Row Name (which you’ve set up to be the same as the item ID).

In the `protected` section, declare an `FName` property named `PickupItemID`. Give it the `EditInstanceOnly` and `Category = “Pickup | Item Table”` specifiers. This is the ID of this pickup in the associated Data Table.

C++

`// The ID of this pickup in the associated data table. UPROPERTY(EditInstanceOnly, Category = "Pickup | Item Table") FName PickupItemID;`

// The ID of this pickup in the associated data table. UPROPERTY(EditInstanceOnly, Category = "Pickup | Item Table") FName PickupItemID;

Copy full snippet(3 lines long)

Pickups shouldn’t have a default item ID, so the `EditInstanceOnly` specifier enables you to edit this property in instances of pickups in the world, but not in the archetype (or class default).

In the `Category` text, the vertical bar (`|`) creates a nested subsection. So in this example, Unreal Engine creates a **Pickup** section with a subsection named **Item Table** in the asset’s **Details** panel.

Next, declare `aTSoftObjectPtr` to a `UDataTable` named `PickupDataTable`. Give it the same specifiers as the `PickupItemID`. This is the Data Table the pickup uses to get its data.

The Data Table may not be loaded at runtime, so use a `TSoftObjectPtr` here so you can load it asynchronously.

Save the header file and switch to `PickupBase.cpp` to implement `InitializePickup()`.  

Inside the function, in an `if` statement, check if the provided `PickupDataTable` is valid and that `PickupItemID` has a value. 

C++

`/**  *	Initializes the pickup with default values by retrieving them from the associated data table. */ void APickupBase::InitializePickup() { 	if (PickupDataTable && !PickupItemID.IsNone()) 	{ 	} }`

/\*\* \* Initializes the pickup with default values by retrieving them from the associated data table. \*/ void APickupBase::InitializePickup() { if (PickupDataTable && !PickupItemID.IsNone()) { } }

Copy full snippet(9 lines long)

In the `if` statement, add code to retrieve the row of values from the Data Table. Declare a const `FItemData` pointer named `ItemDataRow` and set it to the result of calling `FindRow()` on your `PickupDataTable`. Specify `FItemData` as the type of row to find.

C++

`const FItemData* ItemDataRow = PickupDataTable->FindRow<FItemData>();`

const FItemData\* ItemDataRow = PickupDataTable->FindRow<FItemData>();

Copy full snippet(1 line long)

`FindRow()` takes two arguments:

-   An `FName` row name you want to find.  Pass the `PickupItemID` as the row name.  
    
-   An `FString` type context string that you can use for debugging if the row isn’t found.  You can `Text(“My context here.”)` to add a context string, or use `ToString()` to convert the item ID into a context string.     
    

C++

`if (PickupDataTable && !PickupItemID.IsNone()) { 	// Retrieve the item data associated with this pickup from the Data Table 	const FItemData* ItemDataRow = PickupDataTable->FindRow<FItemData>(PickupItemID, PickupItemID.ToString()); }`

if (PickupDataTable && !PickupItemID.IsNone()) { // Retrieve the item data associated with this pickup from the Data Table const FItemData\* ItemDataRow = PickupDataTable->FindRow<FItemData>(PickupItemID, PickupItemID.ToString()); }

Copy full snippet(5 lines long)

### Create a Reference Item

Once you’ve retrieved the pickup’s row data, create and initialize a Data Asset-type `ReferenceItem` to hold that information. 

By saving the data in a reference item like this, Unreal Engine can easily reference that data when it needs to know about the item instead of performing more table data lookups, which is less efficient.

In `PickupBase.h`, in the `protected` section, declare a `TObjectPtr` to a `UItemDefinition` named `ReferenceItem`. This is a Data Asset that stores the pickup’s data. Give it the `VisibleAnywhere` and `Category = “Pickup | Reference Item”` specifiers.

C++

`// Data asset associated with this item. UPROPERTY(VisibleAnywhere, Category = "Pickup | Reference Item") TObjectPtr<UItemDefinition> ReferenceItem;`

// Data asset associated with this item. UPROPERTY(VisibleAnywhere, Category = "Pickup | Reference Item") TObjectPtr<UItemDefinition> ReferenceItem;

Copy full snippet(3 lines long)

Save the header file and switch back to `PickupBase.cpp`.

In `InitializePickup()`, after the `FindRow()` call, set `ReferenceItem` to a `NewObject` of type `UItemDefinition`.

In Unreal Engine, `NewObject<T>()` is a templated function for dynamically creating `UObject`\-derived instances at runtime. It returns a pointer to the new object. It usually has the following syntax:

`*T** Object = NewObject<*T*>(*Outer*, *Class*);`

Where *T* is the type of `UObject` you're creating, *`Outer`* is who owns this object, and *`Class`* is the class of the object you're creating. The `*Class*` argument is often `T::StaticClass()`, which gives a `UClass` pointer representing *T*'s class type. However, you can often omit both arguments as UE assumes *`Outer`* is the current class and uses *T* to infer the `UClass`.

Pass `this` as the outer class and the `UItemDefinition::StaticClass()` as the class type to create a base `UItemDefinition`.

C++

`ReferenceItem = NewObject<UItemDefinition>(this, UItemDefinition::StaticClass());`

ReferenceItem = NewObject<UItemDefinition>(this, UItemDefinition::StaticClass());

Copy full snippet(1 line long)

To copy the pickup’s information into `ReferenceItem`, set each field in `ReferenceItem` to the associated field from `ItemDataRow`. For the `WorldMesh`, pull the `WorldMesh` property from the `ItemBase` that’s referenced in `ItemDataRow`. 

C++

`ReferenceItem = NewObject<UItemDefinition>(this, UItemDefinition::StaticClass());  ReferenceItem->ID = ItemDataRow->ID; ReferenceItem->ItemType = ItemDataRow->ItemType; ReferenceItem->ItemText = ItemDataRow->ItemText; ReferenceItem->WorldMesh = ItemDataRow->ItemBase->WorldMesh;`

ReferenceItem = NewObject<UItemDefinition>(this, UItemDefinition::StaticClass()); ReferenceItem->ID = ItemDataRow->ID; ReferenceItem->ItemType = ItemDataRow->ItemType; ReferenceItem->ItemText = ItemDataRow->ItemText; ReferenceItem->WorldMesh = ItemDataRow->ItemBase->WorldMesh;

Copy full snippet(6 lines long)

### Call InitializePickup()

In `BeginPlay()`, call `InitializePickup()` to initialize the pickup when the game begins. 

C++

`// Called when the game starts or when spawned void APickupBase::BeginPlay() { 	Super::BeginPlay();  	// Initialize this pickup with default values 	InitializePickup(); }`

// Called when the game starts or when spawned void APickupBase::BeginPlay() { Super::BeginPlay(); // Initialize this pickup with default values InitializePickup(); }

Copy full snippet(8 lines long)

Save the file. `PickupBase.cpp` should now look like this:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "PickupBase.h"  // Sets default values APickupBase::APickupBase() {  	// Set this actor to call Tick() every frame. 	PrimaryActorTick.bCanEverTick = true; }`

```

Expand codeCopy full snippet(44 lines long)

## Create In-Game Functionality

Your pickup has the item data it needs, but it still needs to know how to appear and operate in the game world. It needs a mesh for the player to see, a collision volume to determine when the player touches it, and some logic to make the pickup disappear (as if the player picked it up) and respawn after a certain amount of time. 

### Add a Mesh Component

Just like you did when setting up the player character in [Add a First-Person Camera, Mesh, and Animation](https://dev.epicgames.com/documentation/en-us/unreal-engine/adding-a-firstperson-camera-mesh-and-animation), you’ll use the `CreateDefaultSubobject` template function to create a static mesh object as a child component of your pickup class and then apply the item’s mesh to this component.

In `PickupBase.h`, in the `protected` section, declare a `TObjectPtr` to a `UStaticMeshComponent` named `PickupMeshComponent`. This is the mesh that will represent the pickup in the world. 

You’ll use code to assign the Data Asset’s mesh to this property, so give it the `VisibleDefaultsOnly` and `Category = “Pickup | Mesh”` specifiers so it’s visible, but not editable, in Unreal Editor. 

C++

`// The mesh component to represent this pickup in the world. UPROPERTY(VisibleDefaultsOnly, Category = "Pickup | Mesh") TObjectPtr<UStaticMeshComponent> PickupMeshComponent;`

// The mesh component to represent this pickup in the world. UPROPERTY(VisibleDefaultsOnly, Category = "Pickup | Mesh") TObjectPtr<UStaticMeshComponent> PickupMeshComponent;

Copy full snippet(3 lines long)

Save the header file and switch to `PickupBase.cpp`.

In the `APickupBase` construction function, set the `PickupMeshComponent` pointer to the result of calling `CreateDefaultSubobject()` of type `UStaticMeshComponent`. In the `Text` argument, name the object `“PickupMesh”`. 

Then, to ensure the mesh was properly instantiated, check that `PickupMeshComponent` isn’t null. 

C++

`// Sets default values APickupBase::APickupBase() {  	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;  	 // Create this pickup's mesh component 	PickupMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("PickupMesh")); 	check(PickupMeshComponent != nullptr); }`

// Sets default values APickupBase::APickupBase() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Create this pickup's mesh component PickupMeshComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("PickupMesh")); check(PickupMeshComponent != nullptr); }

Copy full snippet(10 lines long)

Go to `InitializePickup()`’s implementation.

Before you apply the `WorldMesh` to the pickup’s mesh component, you’ll need to check that the mesh is loaded since you defined it with a `TSoftObjectPtr`.  

First, declare a new `UItemDefinition` pointer named `TempItemDefinition` and set it to the result of calling `ItemDataRow->ItemBase.Get()`.

C++

`UItemDefinition* TempItemDefinition = ItemDataRow->ItemBase.Get();`

UItemDefinition\* TempItemDefinition = ItemDataRow->ItemBase.Get();

Copy full snippet(1 line long)

Then, in an `if` statement, check if `WorldMesh` is currently loaded by calling `WorldMesh.IsValid()`.

C++

`// Check if the mesh is currently loaded by calling IsValid(). if (TempItemDefinition->WorldMesh.IsValid()) {  }`

// Check if the mesh is currently loaded by calling IsValid(). if (TempItemDefinition->WorldMesh.IsValid()) { }

Copy full snippet(3 lines long)

If it is, set the `PickupMeshComponent` by calling `SetStaticMesh()`, retrieving the `WorldMesh` using `Get()`:

C++

`// Check if the mesh is currently loaded by calling IsValid(). if (TempItemDefinition->WorldMesh.IsValid()) { // Set the pickup's mesh to the associated item's mesh PickupMeshComponent->SetStaticMesh(TempItemDefinition->WorldMesh.Get()); }`

// Check if the mesh is currently loaded by calling IsValid(). if (TempItemDefinition->WorldMesh.IsValid()) { // Set the pickup's mesh to the associated item's mesh PickupMeshComponent->SetStaticMesh(TempItemDefinition->WorldMesh.Get()); }

Copy full snippet(5 lines long)

If the mesh isn't loaded, force it to load by calling `LoadSynchronous()` on the mesh. This function loads and returns an asset pointer to that object. 

After the `if` statement, in an `else` statement, declare a new `UStaticMesh` pointer named `WorldMesh` and set it by calling `WorldMesh.LoadSynchronous()`.

Then, set the `PickupMeshComponent` using `SetStaticMesh()`.

C++

`else { 	// If the mesh isn't loaded, load it by calling LoadSynchronous(). 	UStaticMesh* WorldMesh = TempItemDefinition->WorldMesh.LoadSynchronous(); 	PickupMeshComponent->SetStaticMesh(WorldMesh); }`

else { // If the mesh isn't loaded, load it by calling LoadSynchronous(). UStaticMesh\* WorldMesh = TempItemDefinition->WorldMesh.LoadSynchronous(); PickupMeshComponent->SetStaticMesh(WorldMesh); }

Copy full snippet(5 lines long)

After the `else` statement, make the `PickupMeshComponent` visible using `SetVisiblity(true)`:

C++

`// Set the mesh to visible. PickupMeshComponent->SetVisibility(true);`

// Set the mesh to visible. PickupMeshComponent->SetVisibility(true);

Copy full snippet(2 lines long)

### Add a Collision Shape

Add a sphere component to act as a collision volume, then enable collision queries on that component.

In `PickupBase.h`, in the `protected` section, declare a `TObjectPtr` to a `USphereComponent` named `SphereComponent`. This is the sphere component used for collision detection. Give it the `EditAnywhere`, `BlueprintReadOnly`, and `Category = “Pickup | Components”` specifiers. 

C++

`// Sphere Component that defines the collision radius of this pickup for interaction purposes. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Pickup | Components") TObjectPtr<USphereComponent> SphereComponent;`

// Sphere Component that defines the collision radius of this pickup for interaction purposes. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Pickup | Components") TObjectPtr<USphereComponent> SphereComponent;

Copy full snippet(3 lines long)

Save the header file and switch to `PickupBase.cpp`.

In the `APickupBase` construction function, after you set the `PickupMeshComponent`, set `SphereComponent` to the result of calling `CreateDefaultSubobject` with `USphereComponent` as the type and `“SphereComponent”` as the name. Add a null `check` afterwards. 

C++

`// Create this pickup's sphere component SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); check(SphereComponent != nullptr);`

// Create this pickup's sphere component SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("SphereComponent")); check(SphereComponent != nullptr);

Copy full snippet(3 lines long)

Now that you have both components, use `SetupAttachment()` to attach the `PickupMeshComponent` to the `SphereComponent`:

C++

`// Attach the sphere component to the mesh component SphereComponent->SetupAttachment(PickupMeshComponent);`

// Attach the sphere component to the mesh component SphereComponent->SetupAttachment(PickupMeshComponent);

Copy full snippet(2 lines long)

After attaching the `SphereComponent` to the `MeshComponent`, set the sphere’s size using `SetSphereRadius()`. This value should make your pickup collider large enough to collide with, but not so large that your character accidentally bumps into it.

C++

`// Set the sphere's collision radius SphereComponent->SetSphereRadius(32.f);`

// Set the sphere's collision radius SphereComponent->SetSphereRadius(32.f);

Copy full snippet(2 lines long)

In `InitializePickup()`, after the `SetVisibility(true)` line, make the `SphereComponent` collidable by calling `SetCollisionEnabled()`. 

This function takes an enum (`ECollisionEnabled`) that tells the engine what type of collision to use. You want the character to be able to collide and trigger collision queries with the pickup, but the pickup shouldn’t have any physics that makes it bounce away when hit, so pass the `ECollisionEnabled::QueryOnly` option. 

C++

`// Set the mesh to visible and collidable. PickupMeshComponent->SetVisibility(true); SphereComponent->SetCollisionEnabled(ECollisionEnabled::QueryOnly);`

// Set the mesh to visible and collidable. PickupMeshComponent->SetVisibility(true); SphereComponent->SetCollisionEnabled(ECollisionEnabled::QueryOnly);

Copy full snippet(3 lines long)

  `PickupBase.cpp` should now look like this:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "PickupBase.h" #include "ItemDefinition.h"  // Sets default values APickupBase::APickupBase() { 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;`

```

Expand codeCopy full snippet(79 lines long)

### Simulate Pickup Collisions

Now that your pickup has a collision shape, add logic to detect a collision between the pickup and player and make the pickup disappear when collided with.

#### Set Up the Collision Event

In `PickupBase.h`, in the `protected` section, declare a `void function OnSphereBeginOverlap()`. 

Any component that inherits from `UPrimitiveComponent`, like `USphereComponent`, can implement this function to run code when the component overlaps with some other Actor. This function takes several parameters you won’t be using; you’ll only pass the following:

-   `UPrimitiveComponent* OverlappedComponent`: The component that was overlapped.
    
-   `AActor* OtherActor`: The Actor overlapping that component.
    
-   `UPrimitiveComponent* OtherComp`: The Actor’s component that overlapped.
    
-   `int32 OtherBodyIndex`: The index of the overlapped component.
    
-   `bool bFromSweep, const FHitResult& SweepResult`: Information about the collision, such as where it happened and at what angle.
    

C++

`// Code for when something overlaps the SphereComponent.  UFUNCTION() void OnSphereBeginOverlap(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);`

// Code for when something overlaps the SphereComponent. UFUNCTION() void OnSphereBeginOverlap(UPrimitiveComponent\* OverlappedComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);

Copy full snippet(3 lines long)

Save the header file and switch to `PickupBase.cpp`.

Unreal Engine’s collision events are implemented using dynamic multicast delegates. In UE, this delegate system enables one object to call multiple functions at once, sort of like broadcasting a message to a mailing list where your subscribers are these other functions. When we bind functions to the delegate, it’s like we’re subscribing them to our mailing list. The “delegate” is our event; in this case, a collision between the player and the pickup. When the event happens, Unreal Engine calls all functions bound to that event. 

Unreal Engine includes a couple of other binding functions, but you’ll want to use `AddDynamic()` because your delegate, `OnComponentBeginOverlap`, is a dynamic delegate. And, you’re binding a `UFUNCTION` in a `UObject`class, requiring `AddDynamic()` for reflection support. For more information about dynamic multicast delegates, see Multicast Delegates[Multi-cast Delegates](https://dev.epicgames.com/documentation/en-us/unreal-engine/multicast-delegates-in-unreal-engine).  

In PickupBase.cpp, in `InitializePickup()`, use the `AddDynamic` macro to bind `OnSphereBeginOverlap()` to the sphere component’s `OnComponentBeginOverlap` event. 

C++

`// Register the Overlap Event SphereComponent->OnComponentBeginOverlap.AddDynamic(this, &APickupBase::OnSphereBeginOverlap);`

// Register the Overlap Event SphereComponent->OnComponentBeginOverlap.AddDynamic(this, &APickupBase::OnSphereBeginOverlap);

Copy full snippet(2 lines long)

Save your work. Now, `OnSphereBeginOverlap()` runs when a character collides with the pickup’s sphere component. 

#### Hide the Pickup After a Collision

In `PickupBase.cpp`, implement `OnSphereBeginOverlap()` to make your pickup disappear so it looks like the player picked it up.

Start by adding a debug message to signal when this function is triggered.

C++

`void APickupBase::OnSphereBeginOverlap(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult) { 	GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Attempting a pickup collision")); }`

void APickupBase::OnSphereBeginOverlap(UPrimitiveComponent\* OverlappedComponent, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult) { GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Attempting a pickup collision")); }

Copy full snippet(4 lines long)

Because this function runs whenever another actor collides with the pickup, you need to make sure it’s your first-person character doing the colliding. 

Declare a new `AAdventureCharacter` pointer named `Character` and set it by casting `OtherActor` to your Character class’ name (this tutorial uses `AAdventureCharacter`). 

C++

`// Checking if it's an AdventureCharacter overlapping AAdventureCharacter* Character = Cast<AAdventureCharacter>(OtherActor);`

// Checking if it's an AdventureCharacter overlapping AAdventureCharacter\* Character = Cast<AAdventureCharacter>(OtherActor);

Copy full snippet(2 lines long)

In an `if` statement, check if `Character` is not null. Null indicates that the cast failed and that `OtherActor` was not some type of `AAdventureCharacter`. 

Inside the `if` statement, unregister `OnComponentBeginOverlap` from this function by calling `RemoveAll()` so that it isn’t repeatedly triggered. This ends the collision.

C++

`if (Character != nullptr) { 	// Unregister from the Overlap Event so it is no longer triggered 	SphereComponent->OnComponentBeginOverlap.RemoveAll(this); }`

if (Character != nullptr) { // Unregister from the Overlap Event so it is no longer triggered SphereComponent->OnComponentBeginOverlap.RemoveAll(this); }

Copy full snippet(5 lines long)

Then, set the `PickupMeshComponent` to invisible using `SetVisibility(false)` and set both the pickup mesh and sphere component to non-collidable using `SetCollisionEnabled()`, passing the `NoCollision` option.

C++

`if (Character != nullptr) { 	// Unregister from the Overlap Event so it is no longer triggered 	SphereComponent->OnComponentBeginOverlap.RemoveAll(this);  	// Set this pickup to be invisible and disable collision 	PickupMeshComponent->SetVisibility(false); 	PickupMeshComponent->SetCollisionEnabled(ECollisionEnabled::NoCollision); 	SphereComponent->SetCollisionEnabled(ECollisionEnabled::NoCollision); }`

if (Character != nullptr) { // Unregister from the Overlap Event so it is no longer triggered SphereComponent->OnComponentBeginOverlap.RemoveAll(this); // Set this pickup to be invisible and disable collision PickupMeshComponent->SetVisibility(false); PickupMeshComponent->SetCollisionEnabled(ECollisionEnabled::NoCollision); SphereComponent->SetCollisionEnabled(ECollisionEnabled::NoCollision); }

Copy full snippet(10 lines long)

Save `PickupBase.cpp`.

### Make the Pickup Respawn

Now that the character can’t interact with the pickup, make it respawn after a certain amount of time.

In `PickupBase.h`, in the `protected` section, declare a bool named `bShouldRespawn`. You can use this to turn respawns on or off. 

Declare a `float RespawnTime` initialized to `4.0f`. This is the time to wait until the pickup should respawn.

Give both properties `EditAnywhere`, `BlueprintReadOnly`, and `Category = “Pickup | Respawn”` specifiers.

C++

`// Whether this pickup should respawn after being picked up. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Pickup | Respawn") bool bShouldRespawn;  // The time in seconds to wait before respawning this pickup. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Pickup | Respawn") float RespawnTime = 4.0f;`

// Whether this pickup should respawn after being picked up. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Pickup | Respawn") bool bShouldRespawn; // The time in seconds to wait before respawning this pickup. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Pickup | Respawn") float RespawnTime = 4.0f;

Copy full snippet(7 lines long)

Declare an `FTimerHandle` named `RespawnTimerHandle`. 

C++

`// Timer handle to distinguish the respawn timer. FTimerHandle RespawnTimerHandle;`

// Timer handle to distinguish the respawn timer. FTimerHandle RespawnTimerHandle;

Copy full snippet(2 lines long)

In Unreal Engine, gameplay timers are handled by `FTimerManager`. This class includes the `SetTimer()` function, which calls a function or delegate after a set delay. `FTimerManager’s` functions use an `FTimerHandle` to start, pause, resume, or infinitely loop the function. You’ll use `RespawnTimerHandle` to signal when to respawn the pickup. To learn more about using Timer Manager, see [Gameplay Timers](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-timers-in-unreal-engine).

Save the header file and switch to `PickupBase.cpp`.

To implement the pickup respawn, use the Timer Manager to set a timer that calls `InitializePickup()` after a short wait. 

You only want to respawn the pickup if respawns are enabled; so, at the bottom of  `OnSphereBeginOverlap`, add an `if` statement that checks if `bShouldRespawn` is true.

C++

`if (bShouldRespawn) {  }`

if (bShouldRespawn) { }

Copy full snippet(4 lines long)

In the `if` statement, get the Timer Manager using `GetWorldTimerManager()` and call `SetTimer()` on the timer manager. This function has the following syntax:

`SetTimer(*InOutHandle*, *Object*, *InFuncName*, *InRate*, *bLoop*, *InFirstDelay*);`

Where:

-   `InOutHandle` is the `FTimerHandle` that’s controlling the timer (your `RespawnTimerHandle`).
    
-   `Object` is the `UObject` that owns the function you’re calling. Use this.
    
-   `InFuncName` is a pointer to the function you want to call (`InitializePickup()` in this case).
    
-   `InRate` is a float value specifying the time in seconds to wait before calling your function.
    
-   `bLoop` makes the timer either repeat every `*Time*` seconds (`true`) or only fire once (`false`).
    
-   `InFirstDelay` (optional) is an initial time delay before the first function call in a looping timer. If not specified, UE uses `InRate` as the delay.
    

You only want to call `InitializePickup()` once to replace the pickup, so set `bLoop` to `false`. 

Set your preferred respawn time; this tutorial makes the pickup respawn after four seconds with no initial delay.   

C++

`// If the pickup should respawn, wait an fRespawnTime amount of seconds before calling InitializePickup() to respawn it if (bShouldRespawn) { 	GetWorldTimerManager().SetTimer(RespawnTimerHandle, this, &APickupBase::InitializePickup, 4.0f, false, 0); }`

// If the pickup should respawn, wait an fRespawnTime amount of seconds before calling InitializePickup() to respawn it if (bShouldRespawn) { GetWorldTimerManager().SetTimer(RespawnTimerHandle, this, &APickupBase::InitializePickup, 4.0f, false, 0); }

Copy full snippet(5 lines long)

Your complete `OnSphereBeginOverlap()` function should look like this:

C++

```code
`/**  *	Broadcasts an event when a character overlaps this pickup's SphereComponent. Sets the pickup to invisible and uninteractable, and respawns it after a set time. *	@param OverlappedComponent - the component that was overlapped. *	@param OtherActor - the Actor overlapping this component. *	@param OtherComp - the Actor's component that overlapped this component. *	@param OtherBodyIndex - the index of the overlapped component. *	@param bFromSweep - whether the overlap was generated from a sweep. *	@param SweepResult - contains info about the overlap such as surface normals and faces. */ void APickupBase::OnSphereBeginOverlap(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult)`

```

Expand codeCopy full snippet(33 lines long)

Save your code and compile it from Visual Studio. 

## Implement Pickups in Your Level

Now that you’ve defined the code that makes up your pickups, it’s time to test them out in your game! 

To add pickups to your level, follow these steps:

1.  In Unreal Editor, in the **Content Browser** asset tree, go to **Content > FirstPerson > Blueprints**.
    
2.  In the **Blueprints** folder, create a new child folder named **Pickups** to store your pickup classes.
    
3.  In the asset tree, go to your **C++ Classes** folder. Right-click your **PickupBase** class to create a Blueprint from that class.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/23dfedb2-f547-4b2a-8fe1-669262b76389?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/23dfedb2-f547-4b2a-8fe1-669262b76389?resizing_type=fit)
    
4.  Name it `BP_PickupBase`.
    
5.  For the **Path**, select **Content/FirstPerson/Blueprints/Pickups**, and click **Create Pickup Base Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/a8b839f8-fc28-40c1-b326-5e7ba5dd7ede?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a8b839f8-fc28-40c1-b326-5e7ba5dd7ede?resizing_type=fit)
    
6.  Go back to your **Blueprints > Pickups** folder. Drag your `BP_PickupBase` Blueprint into the level. An instance of PickupBase appears in your level and is automatically selected in the **Outliner** panel. However, it doesn’t have a mesh yet.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2445bec7-b289-4462-995c-93bd3ad6097d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2445bec7-b289-4462-995c-93bd3ad6097d?resizing_type=fit)
    
7.  With the `BP_PickupBase` actor still selected, in the **Details** panel, set the following properties:
    
    1.  Set **Pickup Item ID** to `pickup_001`.
        
    2.  Set **Pickup Data Table** to `DT_PickupData`.
        
    3.  Set **Should Respawn** to **true**.
        
    
    [![](https://dev.epicgames.com/community/api/documentation/image/edd2d50f-1121-4eae-b2f7-4aa053cffcba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/edd2d50f-1121-4eae-b2f7-4aa053cffcba?resizing_type=fit)
    

When you click **Play** to test your game, your pickup uses the **Pickup Item ID** to query the Data Table and retrieve data associated with `pickup_001`. The pickup uses table data and the reference to your `DA_Pickup_001` Data Asset to initialize a reference Item and load its static mesh. 

[![](https://dev.epicgames.com/community/api/documentation/image/a0ade8f9-2036-4653-a47c-79a16e1f115f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a0ade8f9-2036-4653-a47c-79a16e1f115f?resizing_type=fit)

When you run over the pickup, you should see it disappear, then reappear four seconds later. 

### Load a Different Pickup

If you set the **Pickup Item ID** to a different value, your pickup will retrieve data from that row in the table instead. 

To experiment with switching the **Pickup Item ID**, follow these steps: 

1.  Create a new Data Asset named **DA\_Pickup\_002**. Set the following properties in this asset:
    
    -   **ID**: pickup\_002
        
    -   **Item Type**: Consumable
        
    -   **Name**: Test Name 2
        
    -   **Description**: Test Description 2
        
    -   **World** **Mesh**: `SM_ChamferCube`
        
    
    [![500](https://dev.epicgames.com/community/api/documentation/image/59aa75fb-0ca7-4f37-b7e1-8f780626dbc8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/59aa75fb-0ca7-4f37-b7e1-8f780626dbc8?resizing_type=fit)
    
2.  Add a new row in the `DT_PickupData` table and enter the Data Asset's information into the new row's fields.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/75844185-3f50-4127-9ba2-3dba6c631887?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/75844185-3f50-4127-9ba2-3dba6c631887?resizing_type=fit)
    
3.  In the `BP_PickupBase` actor, change the **Pickup Item ID** to `pickup_002`. 
    

When you click **Play** to test your game, the pickup should spawn with the values from `DA_Pickup_002` instead!

[![](https://dev.epicgames.com/community/api/documentation/image/2bed7c14-b80f-43da-a18c-d68f0c4962eb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2bed7c14-b80f-43da-a18c-d68f0c4962eb?resizing_type=fit)

## Update Pickup Actors in the Editor

Your pickups are working in-game, but it can be difficult to visualize them in the editor since they don’t have a default mesh. 

To fix this, use the `PostEditChangeProperty()` function. This is an in-editor function that Unreal Engine calls when the editor changes a property, so you can use it to keep your actors up to date in the Viewport as their properties change. For example, updating a UI element as you change a player’s default health, or scaling a sphere as you bring it closer or further away from the origin. 

In this project, you’ll use it to apply the pickup’s new static mesh whenever **Pickup Item ID** changes. This way, you can change your pickup type and see it immediately update in the Viewport without needing to click Play!

To make changes to your pickups immediately appear in the editor, follow these steps:

1.  In `PickupBase.h`, in the `protected` section, declare an `#if WITH_EDITOR` macro. This macro tells Unreal Header Tool that anything inside it should only be packaged for editor builds and not compiled for release versions of the game. End this macro with an `#endif` statement.
    
    C++
    
    `#if WITH_EDITOR  #endif`
    
    #if WITH\_EDITOR #endif
    
    Copy full snippet(3 lines long)
    
2.  Inside the macro, declare a virtual void function override for `PostEditChangeProperty()`. This function takes a reference to the `FPropertyChangedEvent`, which includes info about the property changed, the type of change, and more. Save the header file.
    
    C++
    
    `#if WITH_EDITOR 	 // Runs whenever a property on this object is changed in the editor 	virtual void PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent) override;  #endif`
    
    #if WITH\_EDITOR // Runs whenever a property on this object is changed in the editor virtual void PostEditChangeProperty(FPropertyChangedEvent&amp; PropertyChangedEvent) override; #endif
    
    Copy full snippet(6 lines long)
    
3.  In `PickupBase.cpp`, implement the `PostEditChangeProperty()` function. Start by calling the `Super::PostEditChangeProperty()` function to handle any parent class property changes.
    
    C++
    
    `/** *	Updates this pickup whenever a property is changed. *	@param PropertyChangedEvent - contains info about the property that was changed. */ void APickupBase::PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent) { 	// Handle parent class property changes 	Super::PostEditChangeProperty(PropertyChangedEvent); }`
    
    /\*\* \* Updates this pickup whenever a property is changed. \* @param PropertyChangedEvent - contains info about the property that was changed. \*/ void APickupBase::PostEditChangeProperty(FPropertyChangedEvent&amp; PropertyChangedEvent) { // Handle parent class property changes Super::PostEditChangeProperty(PropertyChangedEvent); }
    
    Copy full snippet(9 lines long)
    
4.  Create a new `const FName` variable named `ChangedProperty` to store the changed property’s name.
    
    C++
    
    `// Handle parent class property changes Super::PostEditChangeProperty(PropertyChangedEvent);  const FName ChangedPropertyName;`
    
    // Handle parent class property changes Super::PostEditChangeProperty(PropertyChangedEvent); const FName ChangedPropertyName;
    
    Copy full snippet(4 lines long)
    
5.  To verify that the `PropertyChangedEvent` includes a `Property` and save that property, use a ternary operator with `PropertyChangedEvent.Property` as the condition. Set `ChangedPropertyName` to `PropertyChangedEvent.Property->GetFName()` if the condition is true and set it to `NAME_None` if false.
    
    C++
    
    `// If a property was changed, get the name of the changed property. Otherwise use none. const FName ChangedPropertyName = PropertyChangedEvent.Property ? PropertyChangedEvent.Property->GetFName() : NAME_None;`
    
    // If a property was changed, get the name of the changed property. Otherwise use none. const FName ChangedPropertyName = PropertyChangedEvent.Property ? PropertyChangedEvent.Property-&gt;GetFName() : NAME\_None;
    
    Copy full snippet(2 lines long)
    
    `NAME_None` is a global Unreal Engine constant of type `FName` that means "no valid name" or “null name”.
    
6.  Now that you know the name of the property, you can make Unreal Engine update the mesh if it detected the ID changed. 
    
    In an `if` statement, check that the `ChangePropertyName` is equal to the result of calling `GET_MEMBER_NAME_CHECKED()`, passing this `APickupBase` class and the `PickupItemID`. This macro does a compile-time check to ensure the property you pass exists in the passed class.
    
    You’ll be retrieving values from the Data Table as well, so also check that the table is valid before entering the `if` statement.
    
    C++
    
    `// Verify that the changed property exists in this class and that the PickupDataTable is valid. if (ChangedPropertyName == GET_MEMBER_NAME_CHECKED(APickupBase, PickupItemID) && PickupDataTable) { }`
    
    // Verify that the changed property exists in this class and that the PickupDataTable is valid. if (ChangedPropertyName == GET\_MEMBER\_NAME\_CHECKED(APickupBase, PickupItemID) &amp;&amp; PickupDataTable) { }
    
    Copy full snippet(4 lines long)
    
7.  Inside the `if` statement, retrieve the row of data associated with this pickup in the same way you did in `InitializePickup()` by calling `FindRow`.
    
    This time, to ensure the `PickupItemID` is in the table before continuing, put the `FindRow` line in a nested `if` statement.
    
    C++
    
    `// Verify that the changed property exists in this class and that the PickupDataTable is valid. if (ChangedPropertyName == GET_MEMBER_NAME_CHECKED(APickupBase, PickupItemID) && PickupDataTable) { 	// Retrieve the associated ItemData for this pickup. if (const FItemData* ItemDataRow = PickupDataTable->FindRow<FItemData>(PickupItemID, PickupItemID.ToString())) 	{ } }`
    
    // Verify that the changed property exists in this class and that the PickupDataTable is valid. if (ChangedPropertyName == GET\_MEMBER\_NAME\_CHECKED(APickupBase, PickupItemID) &amp;&amp; PickupDataTable) { // Retrieve the associated ItemData for this pickup. if (const FItemData\* ItemDataRow = PickupDataTable-&gt;FindRow&lt;FItemData&gt;(PickupItemID, PickupItemID.ToString())) { } }
    
    Copy full snippet(8 lines long)
    
8.  If UE found the row data successfully, create a `TempItemDefinition` variable to store the Data Asset (that contains the new mesh) that's referenced in the `ItemDataRow`.
    
    C++
    
    `if (const FItemData* ItemDataRow = PickupDataTable->FindRow<FItemData>(PickupItemID, PickupItemID.ToString())) { 	UItemDefinition* TempItemDefinition = ItemDataRow->ItemBase;`
    
    if (const FItemData\* ItemDataRow = PickupDataTable-&gt;FindRow&lt;FItemData&gt;(PickupItemID, PickupItemID.ToString())) { UItemDefinition\* TempItemDefinition = ItemDataRow-&gt;ItemBase;
    
    Copy full snippet(3 lines long)
    
9.  To update the mesh, use `SetStaticMesh` on the `PickupMeshComponent`, passing the temporary Data Asset’s `WorldMesh`.
    
    C++
    
    `// Set the pickup's mesh to the associated item's mesh PickupMeshComponent->SetStaticMesh(TempItemDefinition->WorldMesh.Get());`
    
    // Set the pickup&#39;s mesh to the associated item&#39;s mesh PickupMeshComponent-&gt;SetStaticMesh(TempItemDefinition-&gt;WorldMesh.Get());
    
    Copy full snippet(2 lines long)
    
10.  Set the collision radius of the Sphere Component using `SetSphereRadius(32.f)`.
    
    C++
    
    `// Set the sphere's collision radius SphereComponent->SetSphereRadius(32.f);`
    
    // Set the sphere&#39;s collision radius SphereComponent-&gt;SetSphereRadius(32.f);
    
    Copy full snippet(2 lines long)
    
11.  Save your code and compile it from Visual Studio.
    

Your complete `PostEditChangeProperty()` function should look like this:

C++

```code
`/** *	Updates this pickup whenever a property is changed. *	@param PropertyChangedEvent - contains info about the property that was changed. */ void APickupBase::PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent) { 	// Handle parent class property changes 	Super::PostEditChangeProperty(PropertyChangedEvent);  	// If a property was changed, get the name of the changed property. Otherwise use none.`

```

Expand codeCopy full snippet(28 lines long)

Back in the editor, in the **Outliner**, ensure your **BP\_PickupBase** actor is selected. Change the **Pickup Item ID** from `pickup_001` to `pickup_002`, then change it back. As you change the ID, your pickup’s mesh updates in the Viewport. 

If experimenting with other meshes, you may need to play the game once to force a new mesh to fully load before you can see it in the editor Viewport.

[![](https://dev.epicgames.com/community/api/documentation/image/3ec1f749-e08a-4fb3-92ab-735fc0454e88?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3ec1f749-e08a-4fb3-92ab-735fc0454e88?resizing_type=fit)

## Next Up

Next, you’ll extend your pickup class further to create a custom gadget and equip it to your character!

[

![Equip Your Character](https://dev.epicgames.com/community/api/documentation/image/d7ce94e9-285d-4876-b873-3c7728f842fa?resizing_type=fit&width=640&height=640)

Equip Your Character

Learn to use C++ to create custom equippable items and attach them to your character.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/equip-your-character-with-cplusplus-tools)

## Complete Code

C++

PickupBase.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "Components/SphereComponent.h" #include "CoreMinimal.h" #include "AdventureCharacter.h" #include "GameFramework/Actor.h" #include "PickupBase.generated.h"`


```

Expand codeCopy full snippet(71 lines long)

C++

PickupBase.cpp

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "PickupBase.h" #include "ItemDefinition.h"  // Sets default values APickupBase::APickupBase() { 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;`

```

Expand codeCopy full snippet(147 lines long)