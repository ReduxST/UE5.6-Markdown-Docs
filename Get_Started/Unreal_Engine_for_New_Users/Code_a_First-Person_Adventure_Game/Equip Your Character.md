# Equip Your Character

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/equip-your-character-with-cplusplus-tools](https://dev.epicgames.com/documentation/en-us/unreal-engine/equip-your-character-with-cplusplus-tools)  
**Processed:** 2025-06-14 16:22:32

---

## Before You Begin

Ensure you’ve completed the following objectives in the previous sections: 

-   Built a C++ first-person player character in [Create a Player Character With Input Actions](https://dev.epicgames.com/documentation/en-us/unreal-engine/create-a-player-character-with-input-actions-in-cplusplus).
    
-   Set up data-driven gameplay elements to manage item data in [Manage Items and Data](https://dev.epicgames.com/documentation/en-us/unreal-engine/manage-item-and-data-in-an-unreal-engine-game).
    
-   Created a pickup item and added it to your level in [Create a Respawning Pickup Item](https://dev.epicgames.com/documentation/en-us/unreal-engine/create-a-respawning-pickup-item-in-unreal-engine).
    

### Create Reference Items With a New CreateItemCopy Function

Before you start creating a new equippable pickup item, you’ll first need to modify your **ItemDefinition** and **PickupBase** classes to support capturing a reference item from a wider variety of item types.

In the `InitializePickup()` function in your `PickupBase` class, you set a `ReferenceItem` of type `UItemDefinition`. This is too restrictive; setting a reference item this way won’t include the additional properties you’ll add to any new, specialized item classes derived from `UItemDefinition`. 

To solve this, you’ll create a new virtual function in `ItemDefinition` that creates and returns a copy of that item. Because it’s a virtual function, you can override it in any classes that inherit from `UItemDefinition`. When `PickupBase` calls the function, the compiler determines the correct function to call based on the class it was called from.

Adding this function to the parent `ItemDefinition` class ensures it’s available if you decide to continue extending your project to include more item types that inherit from `UItemDefinition`. 

To define a new `CreateItemCopy()` function for creating reference items, follow these steps:

1.  Open `ItemDefinition.h`. In the `public` section, declare a new virtual const function named `CreateItemCopy()` that returns a `UItemDefinition` pointer.
    
    C++
    
    `// Creates and returns a copy of the item. virtual UItemDefinition* CreateItemCopy() const;`
    
    // Creates and returns a copy of the item. virtual UItemDefinition\* CreateItemCopy() const;
    
    Copy full snippet(2 lines long)
    
2.  In `ItemDefinition.cpp`, implement the `CreateItemCopy()` function. Inside, create a new `UItemDefinition` object pointer named `ItemCopy` using the `StaticClass()`.
    
    C++
    
    `UItemDefinition* UItemDefinition::CreateItemCopy() const  { 	UItemDefinition* ItemCopy = NewObject<UItemDefinition>(StaticClass()); }`
    
    UItemDefinition\* UItemDefinition::CreateItemCopy() const { UItemDefinition\* ItemCopy = NewObject&lt;UItemDefinition&gt;(StaticClass()); }
    
    Copy full snippet(4 lines long)
    
      Visual Studio disambiguates `UItemDefinition::StaticClass()` to `StaticClass()`. 
3.  Assign each field of `ItemCopy` to this class’s fields and then return `ItemCopy`:
    
    C++
    
    ```code
    `/**  *	Creates and returns a copy of this Item Definition. *	@return	a copy of the item. */ UItemDefinition* UItemDefinition::CreateItemCopy() const  { 	UItemDefinition* ItemCopy = NewObject<UItemDefinition>(StaticClass());  	ItemCopy->ID = this->ID; 	ItemCopy->ItemType = this->ItemType;`
    
    ```
    
    Expand codeCopy full snippet(15 lines long)
    

Next, refactor your `InitializePickup()` function by removing the code that manually sets up `ReferenceItem` and replace that code with a `CreateItemCopy()` call.

To update `InitializePickup()` with your new `CreateItemCopy()` function, follow these steps:

1.  Open `PickupBase.cpp` and go to `InitializePickup()`.
    
2.  Delete these five lines that define and set `ReferenceItem`:
    
    C++
    
    `ReferenceItem = NewObject<UItemDefinition>(this, UItemDefinition::StaticClass());  ReferenceItem->ID = ItemDataRow->ID; ReferenceItem->ItemType = ItemDataRow->ItemType; ReferenceItem->ItemText = ItemDataRow->ItemText; ReferenceItem->WorldMesh = ItemDataRow->ItemBase->WorldMesh;`
    
    ReferenceItem = NewObject&lt;UItemDefinition&gt;(this, UItemDefinition::StaticClass()); ReferenceItem-&gt;ID = ItemDataRow-&gt;ID; ReferenceItem-&gt;ItemType = ItemDataRow-&gt;ItemType; ReferenceItem-&gt;ItemText = ItemDataRow-&gt;ItemText; ReferenceItem-&gt;WorldMesh = ItemDataRow-&gt;ItemBase-&gt;WorldMesh;
    
    Copy full snippet(6 lines long)
    
3.   In`ReferenceItem` by calling `TempItemDefinition->CreateItemCopy()`:
    
    C++
    
    `// Create a copy of the item with the class type ReferenceItem = TempItemDefinition->CreateItemCopy();`
    
    // Create a copy of the item with the class type ReferenceItem = TempItemDefinition-&gt;CreateItemCopy();
    
    Copy full snippet(2 lines long)
    

Save `PickupBase.cpp`. Your `InitializePickup()` function should now look like the following:

C++

`if (PickupDataTable && !PickupItemID.IsNone()) { 	// Retrieve the item data associated with this pickup from the data table 	const FItemData* ItemDataRow = PickupDataTable->FindRow<FItemData>(PickupItemID, PickupItemID.ToString());  	UItemDefinition* TempItemDefinition = ItemDataRow->ItemBase.Get();  	// Create a copy of the item with the class type 	ReferenceItem = TempItemDefinition->CreateItemCopy(); }`

if (PickupDataTable && !PickupItemID.IsNone()) { // Retrieve the item data associated with this pickup from the data table const FItemData\* ItemDataRow = PickupDataTable->FindRow<FItemData>(PickupItemID, PickupItemID.ToString()); UItemDefinition\* TempItemDefinition = ItemDataRow->ItemBase.Get(); // Create a copy of the item with the class type ReferenceItem = TempItemDefinition->CreateItemCopy(); }

Copy full snippet(10 lines long)

## Define Equippable Tool Data

In the previous section, you learned how to create interactable pickup objects in your level that are concrete representations of table data. In this section, you’ll learn how to build tools for your character to equip.

To set up a new equippable tool, you’ll create: 

-   `EquippableToolDefinition`: A Data Asset class derived from `ItemDefinition` that stores the tool’s data.
    
-   `EquippableToolBase`: An Actor class to represent the tool in-game. It gives your character the animations, input mappings, and mesh so the character can hold and operate the tool.
    

To make your character able to pick up and equip tools, you’ll add: 

-   A place to store items.
    
-   A way to know the type of each item in their inventory.
    
-   A way to equip tools.
    

Remember, the `EquippableToolBase` actor represents the tool your character is holding and using, while the `PickupBase` actor represents the pickup item in your level. Your character has to collide with the pickup item before it can equip it, so you’ll also modify `PickupBase` to grant the item to the character after a successful collision.      

Then, you’ll combine your new tool class with the pickups and Data Table you’ve already built to create a custom dart launcher and attach it to your character!

First, you’ll define your tool’s data in a new `ItemDefinition` class.

To create a new `EquippableToolDefinition` class, follow these steps:

1.  In Unreal Editor, go to **Tools > New C++ Class**. Go to **All Classes**, search for and select **ItemDefinition** as the parent class, and click **Next**. 
    
    [![](https://dev.epicgames.com/community/api/documentation/image/85dfbedb-adba-40cb-b9bd-be25cd1b8a18?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/85dfbedb-adba-40cb-b9bd-be25cd1b8a18?resizing_type=fit)
    
2.  Name the class `EquippableToolDefinition` and click **Create Class**. 
    
3.  In Visual Studio, at the top of `EquippableToolDefinition.h`, add an include for `”ItemDefinition.h”`, then add the following forward declarations: 
    
    1.  `class UInputMappingContext`: Each equippable tool should hold a reference to an Input Mapping Context that you’ll apply to the character wielding that tool.
        
    2.  `class AEquippableToolBase`: The Actor representing your tools in-game. You’ll create this in the next step. 
        
        C++
        
        ```code
        `#pragma once  #include "CoreMinimal.h" #include "ItemDefinition.h" #include "EquippableToolDefinition.generated.h"  class AEquippableToolBase; class UInputMappingContext;  UCLASS(BlueprintType, Blueprintable)`
        
        ```
        
        Expand codeCopy full snippet(11 lines long)
        
4.  In the `public` section, add a `TSubclassOf` property of type `AEquippableToolBase` named `ToolAsset`. Give this a `UPROPERTY()` macro with `EditDefaultsOnly`.
    
    C++
    
    `// The tool actor associated with this item UPROPERTY(EditDefaultsOnly) TSubclassOf<AEquippableToolBase> ToolAsset;`
    
    // The tool actor associated with this item UPROPERTY(EditDefaultsOnly) TSubclassOf&lt;AEquippableToolBase&gt; ToolAsset;
    
    Copy full snippet(3 lines long)
    
    `TSubclassOf<AEquippableToolBase>` is a template wrapper around `UClass` that enables you to reference Blueprint subclasses of `AEquippableToolBase` while ensuring type safety. It’s useful in gameplay scenarios where you want to spawn different types of actors dynamically.
    
    You’ll use `ToolAsset` to dynamically spawn a tool actor when it gets equipped to your character.
    
5.  Declare an override for the `CreateItemCopy()` function you declared in `UItemDefinition`. This override creates and returns a copy of the `UEquippableToolDefinition` class. 
    
    Your complete `EquippableToolDefinition.h` file should look like the following:
    
    C++
    
    ```code
    `// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "ItemDefinition.h" #include "EquippableToolDefinition.generated.h"  class AEquippableToolBase; class UInputMappingContext;`
    
    ```
    
    Expand codeCopy full snippet(27 lines long)
    
6.  In `EquippableToolDefinition.cpp`, implement the `CreateItemCopy()` function. This should look similar to the `CreateItemCopy()` function in `ItemDefinition.cpp`, except you’ll now also copy the `ToolAsset`. 
    
    C++
    
    ```code
    `// Copyright Epic Games, Inc. All Rights Reserved.  #include "EquippableToolDefinition.h"  UEquippableToolDefinition* UEquippableToolDefinition::CreateItemCopy() const { 	UEquippableToolDefinition* ItemCopy = NewObject<UEquippableToolDefinition>(StaticClass());  	ItemCopy->ID = this->ID; 	ItemCopy->ItemType = this->ItemType;`
    
    ```
    
    Expand codeCopy full snippet(16 lines long)
    

Save both `EquippableToolDefinition` class files.

## Set Up an Equippable Tool Actor

Next, start building your equippable tool Actor. This is the in-game representation that adds the tool’s animations, controls, and mesh to the character. 

To create and set up a new base equippable tool Actor, follow these steps:

1.  In Unreal Editor, go to **Tools > New C++ Class**. Select **Actor** as the parent class and name the class **EquippableToolBase**.
    
2.  Click **Create Class**. Unreal Engine automatically opens your new class’ files in VS.
    
3.  At the top of `EquippableToolBase.h`, forward declare class `AAdventureCharacter` and class `UInputAction`. The equippable tool needs to know what Character it's equipped to so it can bind tool-specific Input Actions to that Character.  
    
4.  In the class declaration’s `UCLASS` macro, add the `BlueprintType` and `Blueprintable` specifiers to expose this class to Blueprints.
    
    C++
    
    `UCLASS(BlueprintType, Blueprintable) class ADVENTUREGAME_API AEquippableToolBase : public AActor`
    
    UCLASS(BlueprintType, Blueprintable) class ADVENTUREGAME\_API AEquippableToolBase : public AActor
    
    Copy full snippet(2 lines long)
    

### Declare Tool Animations

In `EquippableToolBase.h`, in the `public` section, add two `TObjectPtr` to `UAnimBlueprint` properties named `FirstPersonToolAnim` and `ThirdPersonToolAnim`. These are the first-person and third-person animations that the character uses when equipped with this tool.

Give these properties a `UPROPERTY()` macro with `EditAnywhere`and `BlueprintReadOnly`.

C++

`// First Person animations UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<UAnimBlueprint> FirstPersonToolAnim;  // Third Person animations UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<UAnimBlueprint> ThirdPersonToolAnim;`

// First Person animations UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<UAnimBlueprint> FirstPersonToolAnim; // Third Person animations UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<UAnimBlueprint> ThirdPersonToolAnim;

Copy full snippet(7 lines long)

### Create the Tool’s Mesh

In `EquippableToolBase.h`, in the `public` section, add a `TObjectPtr` to a `USkeletalMeshComponent` named `ToolMeshComponent`. This is the tool’s skeletal mesh that the character sees when equipped. Give it a `UPROPERTY()` macro with `EditAnywhere` and `BlueprintReadOnly`.

C++

`// Tool Skeletal Mesh UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<USkeletalMeshComponent> ToolMeshComponent;`

// Tool Skeletal Mesh UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<USkeletalMeshComponent> ToolMeshComponent;

Copy full snippet(3 lines long)

In `EquippableToolBase.cpp`, modify the `AEquippableToolBase()` constructor function to create a default `USkeletalMeshComponent` and assign it to `ToolMeshComponent`. Then check if the `ToolMeshComponent` is not null to make sure your tool has a model when it's loaded. 

C++

`AEquippableToolBase::AEquippableToolBase() { 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;  	// Create this tool's mesh component 	ToolMeshComponent = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("ToolMesh")); 	check(ToolMeshComponent != nullptr); }`

AEquippableToolBase::AEquippableToolBase() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Create this tool's mesh component ToolMeshComponent = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("ToolMesh")); check(ToolMeshComponent != nullptr); }

Copy full snippet(9 lines long)

### Declaring the Tool’s Owner

In `EquippableToolBase.h`, in the `public` section, create a `TObjectPtr` to an instance of your Character class named `OwningCharacter`. Give it a `UPROPERTY()` macro with `EditAnywhere` and `BlueprintReadOnly`.

This is the character this tool is currently equipped to.

C++

`// The character holding this tool UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<AAdventureCharacter> OwningCharacter;`

// The character holding this tool UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<AAdventureCharacter> OwningCharacter;

Copy full snippet(3 lines long)

### Declare Input and a Use-Tool Function

Your tool comes with an Input Mapping Context and Input Action that it needs to give the character. 

To add the Input Mapping Context, in the `public` section, declare a `TObjectPtr` to a `UInputMappingContext` named `ToolMappingContext`. Give it a UPROPERTY() macro with `EditAnywhere` and `BlueprintReadOnly`.

C++

`// The input mapping context associated with this tool UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<UInputMappingContext> ToolMappingContext;`

// The input mapping context associated with this tool UPROPERTY(EditAnywhere, BlueprintReadOnly) TObjectPtr<UInputMappingContext> ToolMappingContext;

Copy full snippet(3 lines long)

Similar to when you implemented movement controls, you’ll add a function that implements a use-tool action and a new function that binds an input action to the function.

In `EquippableToolBase.h`, in the `public` section, declare two virtual void functions named `Use()` and `BindInputAction()`.

When you implemented character movement controls, you used the InputComponent’s `BindAction()` function threquires you to pass the exact name of the target function. You don’t know the full name of the function yet, so you need a custom `BindInputAction()` function that you can implement in each `EquippableToolBase` subclass to call `BindAction`, passing `*[ToolChildClass]*::Use`.  

The `BindInputAction()` function takes a const `UInputAction` pointer and binds the given input action to the character’s `Use()` function.

C++

`// Use the tool UFUNCTION() virtual void Use();  // Binds the Use function to the owning character UFUNCTION() virtual void BindInputAction(const UInputAction* ActionToBind);`

// Use the tool UFUNCTION() virtual void Use(); // Binds the Use function to the owning character UFUNCTION() virtual void BindInputAction(const UInputAction\* ActionToBind);

Copy full snippet(7 lines long)

In `EquippableToolBase.cpp`, implement the `Use()` and `BindInputAction()` functions. These won’t do anything in the parent class, so you can leave them blank for now. You’ll add logic to these when creating `EquippableToolBase` subclasses; for example, the `Use()` function should include tool-specific actions such as launching a projectile or opening a door.

C++

`void AEquippableToolBase::Use() { }  void AEquippableToolBase::BindInputAction(const UInputAction* ActionToBind) { }`

void AEquippableToolBase::Use() { } void AEquippableToolBase::BindInputAction(const UInputAction\* ActionToBind) { }

Copy full snippet(7 lines long)

Save your code and compile it from VS.

Your `EquippableToolBase.h` file should now look like the following:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "EquippableToolBase.generated.h"  class AAdventureCharacter; class UInputAction;`


```

Expand codeCopy full snippet(61 lines long)

`EquippableToolBase.cpp` should now look like the following:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.   #include "EquippableToolBase.h" #include "AdventureCharacter.h"  AEquippableToolBase::AEquippableToolBase() { 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;`

```

Expand codeCopy full snippet(40 lines long)

## Grant Items to a Character

You’ve defined tools your character can use, but they can't equip them yet. Next, you'll add an inventory system so the character can store and equip items when picking them up.

### Build an Inventory Component

Your character’s inventory should add functionality to the character but not exist in the game world, so you’ll use an **Actor Components** class to define an inventory that knows what items a character has, can swap tools, and can prevent the character from obtaining more than one of the same tool. 

In Unreal Editor, go to **Tools > New C++ Class**. Select **Actor Component** as the parent class and name the class `InventoryComponent`. Click **Create Class**. 

[![](https://dev.epicgames.com/community/api/documentation/image/613a3d06-5fa1-412a-84e1-940e81c28a82?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/613a3d06-5fa1-412a-84e1-940e81c28a82?resizing_type=fit)

In VS, at the top of `InventoryComponent.h`, forward declare a `UEquippableToolDefinition`. This is the class you’ll be storing in your inventory.

C++

```code
`#include "CoreMinimal.h" #include "Components/ActorComponent.h" #include "InventoryComponent.generated.h"  class UEquippableToolDefinition;  UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent) ) class ADVENTUREGAME_API UInventoryComponent : public UActorComponent { 	GENERATED_BODY()`

```

Expand codeCopy full snippet(11 lines long)

In the `public` section, declare a new `TArray` of  `UEquippableToolDefinition` pointers named `ToolInventory`. Give this the `UPROPERTY()` macro with `VisibleAnywhere`, `BlueprintReadOnly`, and `Category = Tools`.

C++

`public:	 	// Sets default values for this component's properties 	UInventoryComponent();  	// The array of tools stored in this inventory. 	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Tools) 	TArray<UEquippableToolDefinition*> ToolInventory;`

public: // Sets default values for this component's properties UInventoryComponent(); // The array of tools stored in this inventory. UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Tools) TArray<UEquippableToolDefinition\*> ToolInventory;

Copy full snippet(7 lines long)

This inventory only stores tools, but you can expand this to include any type of item you want. A more generic implementation would store only `UItemDefinition` or `TSubclassOf<UItemDefinition>` values to build a more complex inventory with UI, icons, sound effects, cost, and other item properties. 

Your complete `InventoryComponent.h` file should now look like the following:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "Components/ActorComponent.h" #include "InventoryComponent.generated.h"  class UEquippableToolDefinition;`


```

Expand codeCopy full snippet(33 lines long)

### Add Tool and Inventory Declarations to the Character

Now that you have a place to store your items, you’re ready to upgrade your character with logic that grants them items. 

To start, at the top of your character’s `.h` file, forward declare the `AEquippableToolBase`, `UEquippableToolDefinition`, and `UInventoryComponent` classes.

C++

```code
`#include "CoreMinimal.h" #include "Camera/CameraComponent.h" #include "EnhancedInputComponent.h" #include "EnhancedInputSubsystems.h"  #include "GameFramework/Character.h" #include "InputActionValue.h" #include "AdventureCharacter.generated.h"  class AEquippableToolBase; class UAnimBlueprint;`

```

Expand codeCopy full snippet(16 lines long)

In the `protected` section, declare a `TObjectPtr` to a `UInputAction` named `UseAction`. This is the “use tool” input action that you’ll bind to the tool’s `Use()` function. 

C++

`// Use Input Actions UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Input) TObjectPtr<UInputAction> UseAction;`

// Use Input Actions UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Input) TObjectPtr<UInputAction> UseAction;

Copy full snippet(3 lines long)

### Create the Character’s Inventory Component

In the character’s `.h` file, in the `public` section, declare a `TObjectPtr` to a `UInventoryComponent` named `InventoryComponent`. Give it a `UPROPERTY()` macro with `VisibleAnywhere` and `Category = Inventory`.

C++

`// Inventory Component UPROPERTY(VisibleAnywhere, Category = Inventory) TObjectPtr<UInventoryComponent> InventoryComponent;`

// Inventory Component UPROPERTY(VisibleAnywhere, Category = Inventory) TObjectPtr<UInventoryComponent> InventoryComponent;

Copy full snippet(3 lines long)

In your character’s constructor function, after you create the Mesh Component subobject, create a default `UInventoryComponent` subobject named `InventoryComponent`. This ensures your inventory is set up properly when the Character spawns.

C++

`// Create an inventory component for the owning player InventoryComponent = CreateDefaultSubobject<UInventoryComponent>(TEXT("InventoryComponent"));`

// Create an inventory component for the owning player InventoryComponent = CreateDefaultSubobject<UInventoryComponent>(TEXT("InventoryComponent"));

Copy full snippet(2 lines long)

### Check Existing Inventory

Before you attach the tool, check if the player already has the tool so you don’t equip it multiple times.

In the character’s `.h` file, in the `public` section, declare a function named `IsToolAlreadyOwned()` that takes a `UEquippableToolDefinition` pointer and returns true if that tool already exists in the player’s inventory.

C++

`// Returns whether or not the player already owns this tool UFUNCTION() bool IsToolAlreadyOwned(UEquippableToolDefinition* ToolDefinition);`

// Returns whether or not the player already owns this tool UFUNCTION() bool IsToolAlreadyOwned(UEquippableToolDefinition\* ToolDefinition);

Copy full snippet(3 lines long)

In your character’s `.cpp` file `AdventureCharacter.cpp`, implement the `IsToolAlreadyOwned()` function. Inside, in a `for` loop, get each tool in the character’s inventory by accessing the `InventoryComponent->ToolInventory` array.

C++

`bool AAdventureCharacter::IsToolAlreadyOwned(UEquippableToolDefinition* ToolDefinition) { 	// Check that the character does not yet have this particular tool 	for (UEquippableToolDefinition* InventoryItem : InventoryComponent->ToolInventory) 	{ 	} }`

bool AAdventureCharacter::IsToolAlreadyOwned(UEquippableToolDefinition\* ToolDefinition) { // Check that the character does not yet have this particular tool for (UEquippableToolDefinition\* InventoryItem : InventoryComponent->ToolInventory) { } }

Copy full snippet(7 lines long)

Then, in an `if` statement, check if the `ToolDefinition->ID` from the tool passed to this function matches the `InventoryItem->ID`. If so, `return true` since the character already owns this tool. Otherwise, after the `for` loop, `return false` because `ToolDefinition` didn’t match any existing inventory items and is therefore a new item.

C++

```code
`bool AAdventureCharacter::IsToolAlreadyOwned(UEquippableToolDefinition* ToolDefinition) { 	// Check that the character does not yet have this particular tool 	for (UEquippableToolDefinition* InventoryItem : InventoryComponent->ToolInventory) 	{ 		if (ToolDefinition->ID == InventoryItem->ID) 		{ 			return true; 		} 	}`

```

Expand codeCopy full snippet(13 lines long)

### Attach a Tool

In your character’s `.h` file, in the `public` section, declare a function named `AttachTool()` that takes a `UEquippableToolDefinition` pointer. This function attempts to equip the tool within the `ToolDefinition` to the player.

C++

`// Attaches and equips a tool to the player UFUNCTION() void AttachTool(UEquippableToolDefinition* ToolDefinition);`

// Attaches and equips a tool to the player UFUNCTION() void AttachTool(UEquippableToolDefinition\* ToolDefinition);

Copy full snippet(3 lines long)

In the `protected` section, declare a `TObjectPtr` to an `AEquippableToolBase` named `EquippedTool`. Give it `VisibleAnywhere`, `BlueprintReadOnly`, and `Category = Tools UPROPERTY()` specifiers. 

C++

`// The currently-equipped tool UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Tools) TObjectPtr<AEquippableToolBase> EquippedTool;`

// The currently-equipped tool UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Tools) TObjectPtr<AEquippableToolBase> EquippedTool;

Copy full snippet(3 lines long)

In your character’s `.cpp` file, implement `AttachTool()`. First, in an `if` statement, check if the Character already has the tool by calling `IsToolAlreadyOwned()`.

C++

`void AAdventureCharacter::AttachTool(UEquippableToolDefinition* ToolDefinition) { 	// Only equip this tool if it isn't already owned 	if (not IsToolAlreadyOwned(ToolDefinition)) 	{ 	} }`

void AAdventureCharacter::AttachTool(UEquippableToolDefinition\* ToolDefinition) { // Only equip this tool if it isn't already owned if (not IsToolAlreadyOwned(ToolDefinition)) { } }

Copy full snippet(7 lines long)

#### Spawn an Item

The `AEquippableToolBase` tool stored inside `ToolDefinition` is an Actor, so it may not be loaded when `AttachTool()` is called. To handle this, you’re going to spawn a new instance of the tool using the `SpawnActor()` function. 

`SpawnActor()` is part of the **UWorld** object, which is the core object that represents the map and the actors in it. Access it by calling the `GetWorld()` function from any Actor. 

In the `if` statement, declare a new `AEquippableToolBase` pointer named **ToolToEquip**. Set this equal to the result of calling `GetWorld()->SpawnActor()`, passing the `ToolDefinition->ToolAsset` as the Actor to spawn and`this->GetActorTransform()` as the location to spawn it.

C++

`// Only equip this tool if it isn't already owned if (not IsToolAlreadyOwned(ToolDefinition)) { 	// Spawn a new instance of the tool to equip 	AEquippableToolBase* ToolToEquip = GetWorld()->SpawnActor<AEquippableToolBase>(ToolDefinition->ToolAsset, this->GetActorTransform()); }`

// Only equip this tool if it isn't already owned if (not IsToolAlreadyOwned(ToolDefinition)) { // Spawn a new instance of the tool to equip AEquippableToolBase\* ToolToEquip = GetWorld()->SpawnActor<AEquippableToolBase>(ToolDefinition->ToolAsset, this->GetActorTransform()); }

Copy full snippet(6 lines long)

When you pass `ToolDefinition->ToolAsset` to `SpawnActor`, UE knows to look at `ToolAsset`’s class type and spawn that type of Actor. (`ToolAsset` is the `EquippableToolBase` Actor associated with that `ToolDefinition`.)

#### Attach an Item to the Character

To attach the spawned tool to your character, declare a new `FAttachementTransformRules` named `AttachementRules`.

`FAttachementTransformRules` is a struct that defines how to handle location, rotation, and scale when attaching. It takes `EAttachmentRules` and a bool `InWeldSimulatedBodies` at the end to tell UE if physics is involved. When true, UE welds both bodies together so they can interact as one when moving around. Some popular attachment rules include `KeepRelative` (maintain relative transform to parent), `KeepWorld` (maintain world transform), and `SnapToTarget` (snap to parent's transform).

In your `AttachmentRoles` definition, add `EAttachmentRule::SnapToTarget` and `true`.

C++

`// Attach the tool to the First Person Character FAttachmentTransformRules AttachmentRules(EAttachmentRule::SnapToTarget, true);`

// Attach the tool to the First Person Character FAttachmentTransformRules AttachmentRules(EAttachmentRule::SnapToTarget, true);

Copy full snippet(2 lines long)

Then, call `ToolToEquip->AttachToActor()` to attach the tool to the character, followed by `ToolToEquip->AttachToComponent()` to attach the tool to the right-hand socket of the first-person mesh component.

`AttachToActor` attaches an Actor to a target parent Actor, and `AttachToComponent` attaches an Actor’s root component to the target component. They have the following syntax:

`MyActor->AttachToActor(ParentActor, AttachmentRules, OptionalSocketName)`

C++

`// Attach the tool to this character, and then the right hand of their first-person mesh ToolToEquip->AttachToActor(this, AttachmentRules); ToolToEquip->AttachToComponent(FirstPersonMeshComponent, AttachmentRules, FName(TEXT("HandGrip_R")));`

// Attach the tool to this character, and then the right hand of their first-person mesh ToolToEquip->AttachToActor(this, AttachmentRules); ToolToEquip->AttachToComponent(FirstPersonMeshComponent, AttachmentRules, FName(TEXT("HandGrip\_R")));

Copy full snippet(3 lines long)

#### Add the Item’s Animations to the Character

Set the animations on the first and third-person meshes using `SetAnimInstanceClass()`, passing the tool’s first-person and third-person animations.

C++

`// Set the animations on the character's meshes. 		FirstPersonMeshComponent->SetAnimInstanceClass(ToolToEquip->FirstPersonToolAnim->GeneratedClass); 		GetMesh()->SetAnimInstanceClass(ToolToEquip->ThirdPersonToolAnim->GeneratedClass);`

// Set the animations on the character's meshes. FirstPersonMeshComponent->SetAnimInstanceClass(ToolToEquip->FirstPersonToolAnim->GeneratedClass); GetMesh()->SetAnimInstanceClass(ToolToEquip->ThirdPersonToolAnim->GeneratedClass);

Copy full snippet(3 lines long)

`SetAnimInstanceClass` dynamically changes the animation Blueprint at runtime for a skeletal mesh and is commonly used when equipping items and weapons with different sets of animations. `GeneratedClass` gets the actual `AnimInstance` class generated from the Blueprint.

#### Add the Item to Inventory

Add the tool to the character’s inventory using `ToolInventory.Add()`.

C++

`// Add the tool to this character's inventory InventoryComponent->ToolInventory.Add(ToolDefinition);`

// Add the tool to this character's inventory InventoryComponent->ToolInventory.Add(ToolDefinition);

Copy full snippet(2 lines long)

Now that the tool is attached, set the `ToolToEquip->OwningCharacter` to this character.

C++

`ToolToEquip->OwningCharacter = this;`

ToolToEquip->OwningCharacter = this;

Copy full snippet(1 line long)

You’ve finished attaching the new tool to the character, so set the `EquippedTool` to `ToolToEquip`.

C++

`EquippedTool = ToolToEquip;`

EquippedTool = ToolToEquip;

Copy full snippet(1 line long)

#### Add an Item’s Controls to the Character

Next, add the tool’s **Input Action** and **Input Mapping Context** to the character. 

You’ll implement this similar to how you set up `AAdventureCharacter::BeginPlay()` in the **Bind the Input Mapping to the Character** section of [Configure Character Movement](https://dev.epicgames.com/documentation/en-us/unreal-engine/configure-character-movement-with-cplusplus-in-unreal-engine): getting the `PlayerController`, then the enhanced input local subsystem, using `if` statements to check for null pointers as you go.

C++

`// Get the player controller for this character if (APlayerController* PlayerController = Cast<APlayerController>(Controller)) { 	if (UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PlayerController->GetLocalPlayer())) 	{ 		Subsystem->AddMappingContext(ToolToEquip->ToolMappingContext, 1); 	} }`

// Get the player controller for this character if (APlayerController\* PlayerController = Cast<APlayerController>(Controller)) { if (UEnhancedInputLocalPlayerSubsystem\* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PlayerController->GetLocalPlayer())) { Subsystem->AddMappingContext(ToolToEquip->ToolMappingContext, 1); } }

Copy full snippet(8 lines long)

This time, when you add the tool’s Input Mapping Context to the player subsystem, set the priority to `1`. The priority of the player’s main mapping context (`FirstPersonContext`) is lower (`0`), so when both mapping contexts have the same key binding, the input binding in `ToolToEquip->ToolMappingContext` takes priority over `FirstPersonContext`.  

After adding the mapping context, call `ToolToEquip->BindInputAction()` passing the `UseAction` to bind the character’s input action to the tool’s `Use()` function.

C++

`// Get the player controller for this character if (APlayerController* PlayerController = Cast<APlayerController>(Controller)) { 	if (UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PlayerController->GetLocalPlayer())) 	{ 		Subsystem->AddMappingContext(ToolToEquip->ToolMappingContext, 1); 	}  	ToolToEquip->BindInputAction(UseAction); }`

// Get the player controller for this character if (APlayerController\* PlayerController = Cast<APlayerController>(Controller)) { if (UEnhancedInputLocalPlayerSubsystem\* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PlayerController->GetLocalPlayer())) { Subsystem->AddMappingContext(ToolToEquip->ToolMappingContext, 1); } ToolToEquip->BindInputAction(UseAction); }

Copy full snippet(10 lines long)

Your complete `AttachTool()` function should look like the following:

C++

```code
`void AAdventureCharacter::AttachTool(UEquippableToolDefinition* ToolDefinition) {  	// Only equip this tool if it isn't already owned 	if (not IsToolAlreadyOwned(ToolDefinition)) 	{ 		// Spawn a new instance of the tool to equip 		AEquippableToolBase* ToolToEquip = GetWorld()->SpawnActor<AEquippableToolBase>(ToolDefinition->ToolAsset, this->GetActorTransform());  		// Attach the tool to the First Person Character`

```

Expand codeCopy full snippet(41 lines long)

### Support Different Item Types with GiveItem()

You’ve got a way to attach tools, but because pickups and their item definitions can contain more than just tools, you need a way to know what kind of item your character is interacting with before calling `AttachTool()`. 

Create a `GiveItem()` function to perform different actions based on the type of `ItemDefinition` passed in. You declared different types of items with the `EItemType enum` in `ItemData.h` and you can use that data now to differentiate between different item definitions.

In `AdventureCharacter.h`, in the `public` section, declare a function named `GiveItem()` that takes a `UItemDefinition()` pointer. Other classes call this function when attempting to give an item to the player.

C++

`// Public function that other classes can call to attempt to give an item to the player UFUNCTION() void GiveItem(UItemDefinition* ItemDefinition);`

// Public function that other classes can call to attempt to give an item to the player UFUNCTION() void GiveItem(UItemDefinition\* ItemDefinition);

Copy full snippet(3 lines long)

In `AdventureCharacter.cpp`, implement `GiveItem()`. Start by declaring a switch statement that cases based on the `ItemType` of the item passed to this function.

C++

`void AAdventureCharacter::GiveItem(UItemDefinition* ItemDefinition) { 	// Case based on the type of the item 	switch (ItemDefinition->ItemType) 	{ 	} }`

void AAdventureCharacter::GiveItem(UItemDefinition\* ItemDefinition) { // Case based on the type of the item switch (ItemDefinition->ItemType) { } }

Copy full snippet(7 lines long)

Inside the switch statement, declare cases for `EItemType::Tool`, `EItemType::Consumable`, and a default case. In this tutorial, you’re only implementing the Tool-type item, so in the `Consumable` and `default` cases, log the type of item and break out of the switch case. 

C++

```code
`// Case based on the type of the item switch (ItemDefinition->ItemType) { case EItemType::Tool: { } case EItemType::Consumable: { 	// Not yet implemented 	break;`

```

Expand codeCopy full snippet(14 lines long)

Inside the `Tool` case, cast the `ItemDefinition` to a `UEquippableToolDefinition` pointer named `ToolDefinition.` 

Then, ensure the cast succeeded by checking if `ToolDefinition` is `null`. If it isn’t `null`, call `AttachTool()` to attach the tool to the character. Otherwise, `print` the error and `break`.

C++

```code
`case EItemType::Tool: { // If the item is a tool, attempt to cast and attach it to the character 	 UEquippableToolDefinition* ToolDefinition = Cast<UEquippableToolDefinition>(ItemDefinition); 	 if (ToolDefinition != nullptr) { 	AttachTool(ToolDefinition); }`

```

Expand codeCopy full snippet(15 lines long)

Your complete `GiveItem()` function should look like the following:

C++

```code
`void AAdventureCharacter::GiveItem(UItemDefinition* ItemDefinition) { 	// Case based on the type of the item 	switch (ItemDefinition->ItemType) 	{  case EItemType::Tool: { 	// If the item is a tool, attempt to cast and attach it to the character`
	

```

Expand codeCopy full snippet(32 lines long)

Last, you need an in-game trigger to set your item-granting logic in motion. When a character collides with a pickup, the pickup should call the character’s `GiveItem()` function to grant the pickup’s `ReferenceItem` to the character.

To do this, open `PickupBase.cpp`.

In `OnSphereBeginOverlap()`, after checking if the Character is valid,  call `Character->GiveItem(ReferenceItem)` to grant the item to your character.

C++

`// Checking if it is a First Person Character overlapping AAdventureCharacter* Character = Cast<AAdventureCharacter>(OtherActor); if (Character != nullptr) { 	// Give the item to the character 	Character->GiveItem(ReferenceItem);    // Unregister from the Overlap Event so it is no longer triggered   SphereComponent->OnComponentBeginOverlap.RemoveAll(this);`

// Checking if it is a First Person Character overlapping AAdventureCharacter\* Character = Cast<AAdventureCharacter>(OtherActor); if (Character != nullptr) { // Give the item to the character Character->GiveItem(ReferenceItem); // Unregister from the Overlap Event so it is no longer triggered SphereComponent->OnComponentBeginOverlap.RemoveAll(this);

Copy full snippet(9 lines long)

Now that you’ve set up your tool data and actor, you can use these to build a real tool for your character to equip in-game!

## Implement a Dart Launcher

For your first equippable tool, you’ll create a dart launcher that can launch projectiles. In this section, you’ll start by creating the tool for your character to hold and use. In the next section of this tutorial, you’ll implement projectile logic. 

### Set up a New DartLauncher Class

In the Unreal Editor, go to **Tools > New C++ Class**. 

Go to **All Classes**, search for and select **EquippableToolBase** as the parent class, and name the class `DartLauncher`. Create a new folder named **Tools** to store the code for your tools. Click **Create Class**. 

In Visual Studio,  at the top of `DartLauncher.h`: 

1.  Add an include statement for `”[ProjectName]/EquippableToolBase.h”`.
    
2.  Add the `BlueprintType` and `Blueprintable` specifiers to the `UCLASS()` macro.
    
3.  In the `public` section, declare overrides for both the `Use()` and `BindInputAction()` functions from `AEquippableToolBase`.
    

Your complete `DartLauncher.h` class should look like the following:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "AdventureGame/EquippableToolBase.h" #include "DartLauncher.generated.h"  UCLASS(BlueprintType, Blueprintable) class ADVENTUREGAME_API ADartLauncher : public AEquippableToolBase`

```

Expand codeCopy full snippet(23 lines long)

In `DartLauncher.cpp`, at the top of the file, add an include statement for `”[ProjectName]/AdventureCharacter.h”`. You’ll need this in the `BindInputAction()` function. 

C++

`#include "DartLauncher.h" #include "AdventureGame/AdventureCharacter.h"`

#include "DartLauncher.h" #include "AdventureGame/AdventureCharacter.h"

Copy full snippet(2 lines long)

### Implement Tool Controls

Now that you’re working in a specific tool and know what function you’re binding, you can implement `BindInputAction()`. 

 First, implement the `Use()` function. Inside `Use()`, add a debug message that notifies when the player triggers the function.

C++

`#include "DartLauncher.h" #include "AdventureGame/AdventureCharacter.h"  void ADartLauncher::Use() { 	GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Using the dart launcher!")); }`

#include "DartLauncher.h" #include "AdventureGame/AdventureCharacter.h" void ADartLauncher::Use() { GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Using the dart launcher!")); }

Copy full snippet(7 lines long)

Next, implement the `BindInputAction()` function. Inside the function, in an `if` statement, get the player controller for the `OwningCharacter` by using `GetController()`, and then cast it to `APlayerController`. This is similar to how you added a mapping context in the `AAdventureCharacter::BeginPlay()` function.

C++

`void ADartLauncher::BindInputAction(const UInputAction* InputToBind) { 	// Set up action bindings 	if (APlayerController* PlayerController = Cast<APlayerController>(OwningCharacter->GetController())) 	{  	} }`

void ADartLauncher::BindInputAction(const UInputAction\* InputToBind) { // Set up action bindings if (APlayerController\* PlayerController = Cast<APlayerController>(OwningCharacter->GetController())) { } }

Copy full snippet(8 lines long)

Just like how you bound your movement actions in the **Binding Movement Actions** section of [Configure Character Movement](https://dev.epicgames.com/documentation/en-us/unreal-engine/configure-character-movement-with-cplusplus-in-unreal-engine): in another `if` statement, declare a new `UEnhancedInputComponent` pointer named **EnhancedInputComponent**. Set this equal to the result of calling `Cast()` on the `PlayerInputComponent` passed to this function while casting it to `UEnhancedInputComponent`. 

Finally, use `BindAction` to bind the `ADartLauncher::Use` action to the `InputToBind` action that’s passed to this function using `BindAction()`. This binds the InputAction to `Use();` so that when the given action happens, `Use()` is called.

C++

`// Set up action bindings if (APlayerController* PlayerController = Cast<APlayerController>(OwningCharacter->GetController())) {  	if (UEnhancedInputComponent* EnhancedInputComponent = Cast<UEnhancedInputComponent>(PlayerController->InputComponent)) 	{ 		// Fire 		EnhancedInputComponent->BindAction(InputToBind, ETriggerEvent::Triggered, this, &ADartLauncher::Use); 	} }`

// Set up action bindings if (APlayerController\* PlayerController = Cast<APlayerController>(OwningCharacter->GetController())) { if (UEnhancedInputComponent\* EnhancedInputComponent = Cast<UEnhancedInputComponent>(PlayerController->InputComponent)) { // Fire EnhancedInputComponent->BindAction(InputToBind, ETriggerEvent::Triggered, this, &ADartLauncher::Use); } }

Copy full snippet(10 lines long)

When you set up your character’s movement, you used `CastChecked<>` which crashes the game if it fails. Here, you don’t want to stop the game if the pickup controls don’t get initialized properly, so just use `Cast<>`. Only use `CastChecked<>` when a failed cast would indicate a serious bug.

Save your code and compile it. 

Your `BindInputAction()` function and your complete `DartLauncher.cpp` class should now look like this:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "DartLauncher.h" #include "AdventureGame/AdventureCharacter.h"  void ADartLauncher::Use() { 	GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Using the dart launcher!"));  }`

```

Expand codeCopy full snippet(34 lines long)

### Adapt an Animation Blueprint For Your Character

The first-person template includes a sample Animation Blueprint for weapon-type items, but you’ll need to make a few changes to the Blueprint so it can work with your dart launcher.

To adapt an existing Animation Blueprint for your character, take the following steps:

1.  In the **Content Browser**, go to the **Content > Variant\_Shooter > Anim** folder, right-click the `ABP_FP_Pistol` Animation Blueprint, and select **Duplicate**.
    
2.  Name this copy **ABP\_FP\_DartLauncher**, drag it into the **Content > FirstPerson > Anims** folder, and select **Move Here**. 
    
    [![](https://dev.epicgames.com/community/api/documentation/image/4c39cc80-07e8-4896-81da-d61e3c7ab24e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4c39cc80-07e8-4896-81da-d61e3c7ab24e?resizing_type=fit)
    
    `ABP_TP_Pistol` doesn’t use any logic specific to the `BP_FPShooter` character; you don’t need to modify it for your character.
    
3.  Near the top of the Event Graph, zoom in to the group of nodes that begins with an **Event Blueprint Begin Play** node.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/20ad9c9f-fa04-4c18-8d93-465c3a48ce30?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/20ad9c9f-fa04-4c18-8d93-465c3a48ce30?resizing_type=fit)
    
    This Blueprint gets **First Person Mesh** and **First Person Camera** variables from `BP_FPShooter`, so you’ll change this to use your Character Blueprint instead (this tutorial uses `BP_AdventureCharacter`).
    
4.  Click each of these nodes and press **Delete**:
    
    -   **Cast To BP\_FPShooter**
        
    -   **First Person Mesh**
        
    -   **First Person Camera**
        
5.  Right-click on the **Event Graph**, then search for and select a **Cast To BP\_AdventureCharacter** node. 
    
    [![](https://dev.epicgames.com/community/api/documentation/image/c92e22d9-c55b-45a9-9555-ea923db02b86?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c92e22d9-c55b-45a9-9555-ea923db02b86?resizing_type=fit)
    
6.  Connect the execution pins from **Event Blueprint Begin Play** to the new node, and then to the **Set First Person Mesh** node. 
    
7.  Connect the **Try Get Pawn Owner** node’s **Return Value** pin to the **Cast To node’s Object** pin.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/90179f66-960a-4701-bdd5-6d6cd5a5aac7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/90179f66-960a-4701-bdd5-6d6cd5a5aac7?resizing_type=fit)
    
8.  To create a new node off of **Cast To BP\_AdventureCharacter**, click the **As BP My Adventure Character** pin and drag to an empty spot in the graph.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/41e6939b-fd9c-4f02-8edf-b3ac56b5c13d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/41e6939b-fd9c-4f02-8edf-b3ac56b5c13d?resizing_type=fit)
    
9.  Search for and **Get Mesh** and select it under **Variables > Character**. Connect the new node’s **Mesh** pin to the **Set First Person Mesh** node.
    
10.  For the camera, drag another node from the **As BP My First Person Character** pin, and search for and select **Get Component by Class**.
    
    Ensure you create a **Get Component by Class** node with “by” in lowercase.
    
11.  On the new node, set the **Component Class** to **Camera Component**. Then, connect the **Return Value** pin to the **Set First Person Camera** node.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f4d9cb01-19db-4a7c-a23e-d28a0668ea29?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f4d9cb01-19db-4a7c-a23e-d28a0668ea29?resizing_type=fit)
    

Save your `ABP_FP_DartLauncher` Blueprint and compile it. 

### Define Dart Launcher Controls

Your dart launcher needs an input action and input mapping context so the character can shoot projectiles from the tool.

To create player controls for your dart launcher tool, follow these steps:

1.  In the **Content Browser**, go to the **Input > Actions** folder.
    
2.  Create and set up a “use tool” Input Action:
    
    1.  Click **Add**, go to **Input**, and select **Input Action**. Name it **IA\_UseTool**.
        
        [![](https://dev.epicgames.com/community/api/documentation/image/e768d7ad-b3f8-4475-b8c7-64f137dbf669?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e768d7ad-b3f8-4475-b8c7-64f137dbf669?resizing_type=fit)
        
    2.  Double-click **IA\_UseTool** to open it. In its **Details** panel, ensure its **Value Type** is **Digital (bool)**.
        
    3.  Next to **Triggers**, click the plus button (+), then select **Pressed** from the list of triggers.
        
        [![](https://dev.epicgames.com/community/api/documentation/image/778c9091-719b-4808-b0d2-ab1c464275cf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/778c9091-719b-4808-b0d2-ab1c464275cf?resizing_type=fit)
        
    4.  Save and close the Input Action.
        
3.  Back in the **Content Browser**, go to the **Input** **folder**.
    
4.  Create and set up a new Input Mapping Context that maps the left mouse button and gamepad right trigger to the dart launcher's Use action:
    
    1.  Create a new **Input Mapping Context** named **IMC\_DartLauncher**.
        
        [![](https://dev.epicgames.com/community/api/documentation/image/9518ad9f-ca19-4bf4-9872-cdfc84bfa4a2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9518ad9f-ca19-4bf4-9872-cdfc84bfa4a2?resizing_type=fit)
        
    2.  Open **IMC\_DartLauncher**. Click the plus button next to **Mappings**.
        
    3.  In the dropdown list, select `IA_UseTool`.
        
    4.  Click the arrow to expand the mapping. Click the keyboard button, then press your left mouse button to bind that button to `IA_UseTool`.
        
    5.  Next to **IA\_UseTool**, click the plus button to add another binding. In the dropdown list, expand **Gamepad** and select **Gamepad Right Trigger Axis**.
        
        [![](https://dev.epicgames.com/community/api/documentation/image/e648a1ed-1848-4383-991d-a98ffb9c0510?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e648a1ed-1848-4383-991d-a98ffb9c0510?resizing_type=fit)
        
    6.  Save and close the Input Mapping Context.
        

### Create the DartLauncher Blueprint

Back in the main editor, in the **Content Browser** asset tree, go to your **C++ Classes** folder, right-click your **DartLauncher** class, and create a new Blueprint class. 

Name it `BP_DartLauncher`. In your **FirstPerson > Blueprints** folder, create a new folder named **Tools** to store your equippable items, then finish creating the Blueprint.

In the Blueprint's **Details** panel, set the following default properties: 

1.  Set **First Person Tool Anim** to `ABP_FP_DartLauncher`.
    
2.  Set **Third Person Tool Anim** to `ABP_TP_Pistol`.
    
3.  Set **Tool Mapping Context** to `IMC_DartLauncher`.
    

[![](https://dev.epicgames.com/community/api/documentation/image/c2389a1f-0be8-40f6-8998-70aa5f64e773?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c2389a1f-0be8-40f6-8998-70aa5f64e773?resizing_type=fit)

If you can only see your Blueprint’s Details panel and not the full Blueprint Editor with Event Graph and Components tab, click **Open Full Blueprint Editor** in the note near the top of the window.

[![](https://dev.epicgames.com/community/api/documentation/image/f34feedd-3a2b-4a1d-b7e1-3eb28ddda023?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f34feedd-3a2b-4a1d-b7e1-3eb28ddda023?resizing_type=fit)

In the **Components** tab, select the **Tool Mesh Component** and set the **Skeletal Mesh Asset** to `SKM_Pistol`.

[![](https://dev.epicgames.com/community/api/documentation/image/8bb52a11-c339-48b6-ae9f-6735fd7cb2f6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8bb52a11-c339-48b6-ae9f-6735fd7cb2f6?resizing_type=fit)

### Create the Dart Launcher Data Asset

To create a Data Asset to store this Blueprint’s data, follow these steps:

1.  In the Content Browser, in the **FirstPerson > Data** folder, create a new Data Asset and pick **Equippable Tool Definition** as the Data Asset instance. Name this asset `DA_DartLauncher`.
    
2.  Inside `DA_DartLauncher`, in the **Details** panel, set the following properties:
    
    -   Set **Tool Asset** to `BP_DartLauncher`.
        
    -   Set **ID** to **tool\_001**.
        
    -   Set **Item Type** to **Tool**.
        
    -   Set **World Mesh** to `SM_Pistol`.
        
    
    [![](https://dev.epicgames.com/community/api/documentation/image/68a2ad76-4607-408f-af3c-f65ffbf2722a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/68a2ad76-4607-408f-af3c-f65ffbf2722a?resizing_type=fit)
    
3.  Enter a **Name** and **Description**.
    
4.  Save your Data Asset.
    

### Create a Data Table for Tools

Although this tool could go in your DT\_PickupData table, it’s helpful to organize your tables to track specific things. For example, you could have different tables for items that specific classes can equip, or tables of items that different enemies drop when defeated. In this tutorial, you’ll have a table for consumables and a table for tools. 

To create a new Data Table to track your tool items, follow these steps:

1.  In the **Content Browser**, go to the **FirstPerson > Data** folder, and create a new **Data** **Table**.
    
2.  Select **ItemData** as the row structure.
    
3.  Name the table **DT\_ToolData**, then double-click it to open it.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/7dd7db4d-018f-44ae-83f6-05a8fbca92bc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7dd7db4d-018f-44ae-83f6-05a8fbca92bc?resizing_type=fit)
    
4.  Inside DT\_ToolData, click **Add** to create a new row for your dart launcher.
    
5.  With the new row selected, set the following fields:
    
    -   Set **Row Name** and ID to **tool\_001**.
        
    -   Set **Item Type** to **Tool**.
        
    -   Set **Item Base** to the `DA_DartLauncher`.
        
    
    [![](https://dev.epicgames.com/community/api/documentation/image/8ee733ed-b82c-4bc5-9255-06f0fc24969e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8ee733ed-b82c-4bc5-9255-06f0fc24969e?resizing_type=fit)
    
6.  Save and close the Data Table.
    

## Test a Dart Launcher Pickup In Game

You’ve modified your pickup class to grant an item to the user, created an equippable item class that gives the player a new mesh, animations, and controls, and set up a dart launcher tool. It’s time to bring it all together and create the in-game pickup that triggers all the equippable item logic you’ve set up in this part of the tutorial.

In the **Content Browser**, go to **Content > FirstPerson > Blueprints** and drag a new `BP_PickupBase` into the level. Set the **Pickup Item ID** to **tool\_001** and the **Pickup Data Table** to `DT_ToolData`.

[![](https://dev.epicgames.com/community/api/documentation/image/9ac914b9-fd50-4bc1-9d96-c0e347418d71?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9ac914b9-fd50-4bc1-9d96-c0e347418d71?resizing_type=fit)

Click **Play** to test out your game. When the game begins, your pickup should initialize to the dart launcher. When you run over your pickup, your character should start holding the tool!

## Next Up

In the final section, you’ll implement projectile physics in your dart launcher and make it launch foam darts!

[

![Implement a Projectile](https://dev.epicgames.com/community/api/documentation/image/25ecf04a-ccd5-4507-80d4-446d937d850c?resizing_type=fit&width=640&height=640)

Implement a Projectile

Learn to use C++ to implement projectiles and spawn them during gameplay.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/implement-a-projectile-in-unreal-engine)

## Complete Code

C++

ItemDefinition.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "ItemData.h" #include "ItemDefinition.generated.h"  /** *	Defines a basic item with a static mesh that can be built from the editor.`

```

Expand codeCopy full snippet(37 lines long)

C++

EquippableToolDefinition.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "ItemDefinition.h" #include "EquippableToolDefinition.generated.h"  class AEquippableToolBase; class UInputMappingContext;`

```

Expand codeCopy full snippet(26 lines long)

C++

EquippableToolDefinition.cpp

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "EquippableToolDefinition.h"  UEquippableToolDefinition* UEquippableToolDefinition::CreateItemCopy() const { 	UEquippableToolDefinition* ItemCopy = NewObject<UEquippableToolDefinition>(StaticClass());  	ItemCopy->ID = this->ID; 	ItemCopy->ItemType = this->ItemType;`

```

Expand codeCopy full snippet(16 lines long)

C++

InventoryComponent.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "Components/ActorComponent.h" #include "InventoryComponent.generated.h"  class UEquippableToolDefinition;`


```

Expand codeCopy full snippet(32 lines long)

C++

DartLauncher.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "AdventureGame/EquippableToolBase.h" #include "DartLauncher.generated.h"  UCLASS(BlueprintType, Blueprintable) class ADVENTUREGAME_API ADartLauncher : public AEquippableToolBase`

```

Expand codeCopy full snippet(23 lines long)

N

C++

DartLauncher.cpp

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "DartLauncher.h" #include "AdventureGame/AdventureCharacter.h"  void ADartLauncher::Use() { 	GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Using the dart launcher!"));  }`

```

Expand codeCopy full snippet(34 lines long)

N

C++

EquippableToolBase.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "EquippableToolBase.generated.h"  class AAdventureCharacter; class UInputAction;`


```

Expand codeCopy full snippet(61 lines long)

C++

EquippableToolBase.cpp

```code
`// Copyright Epic Games, Inc. All Rights Reserved.   #include "EquippableToolBase.h" #include "AdventureCharacter.h"  AEquippableToolBase::AEquippableToolBase() { 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;`

```

Expand codeCopy full snippet(38 lines long)

C++

AdventureCharacter.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "Camera/CameraComponent.h" #include "EnhancedInputComponent.h" #include "EnhancedInputSubsystems.h"  #include "GameFramework/Character.h" #include "InputActionValue.h"`

```

Expand codeCopy full snippet(105 lines long)

C++

AdventureCharacter.cpp

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #include "AdventureCharacter.h" #include "EquippableToolBase.h" #include "EquippableToolDefinition.h" #include "ItemDefinition.h" #include "InventoryComponent.h"  // Sets default values AAdventureCharacter::AAdventureCharacter()`

```

Expand codeCopy full snippet(225 lines long)