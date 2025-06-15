# Manage Items and Data

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/manage-item-and-data-in-an-unreal-engine-game](https://dev.epicgames.com/documentation/en-us/unreal-engine/manage-item-and-data-in-an-unreal-engine-game)  
**Processed:** 2025-06-14 16:34:49

---

## Before You Begin

Ensure you have a C++-based Unreal Engine Project.

This page continues from [Add a First-Person Camera, Mesh, and Animation](https://dev.epicgames.com/documentation/en-us/unreal-engine/adding-a-firstperson-camera-mesh-and-animation); however, you can complete this independently of the rest of the [Code a First-Person Adventure Game](https://dev.epicgames.com/documentation/en-us/unreal-engine/code-a-firstperson-adventure-game-in-unreal-engine) tutorial series if you'd just like to learn about data-driven gameplay.  

## Data Organization in Games

How you organize and represent data is an important part of game design. Interactable items could have very different qualities and can exist in game or just as a piece of data. You could represent this data by creating separate classes and Blueprints for each item type, distributing and communicating data across different Actors. However, this gets inefficient as your game and the amount of stored data grows.

A better approach is **data-driven gameplay**. Instead of hardcoding values, you'll organize data in a centralized location managed by systems in your game. Data-driven gameplay lets you load what you need when you need it. For example, many games use spreadsheet documents to organize dialogue as it's easier for a system to pull a specific line of dialogue instead of storing potentially hundreds of lines in each character.

In this section, you’ll learn how use this methodology to start creating custom items. 

### Data-Driven Gameplay Elements

Before you start building basic items, it’s important to consider what defines an “item”. Since an item can be anything a player interacts with, it should have a minimal set of properties that are valid for any type of item. You’ll set this up in an **Item Data Struct**. You should also have a centralized place to organize and display this item data. For that, you’ll use a **Data Table** asset. 

Your Item Data Struct acts as a template that defines the type of data your item has, then your Data Table and **Data Assets** store the actual data entries based on your struct. 

The diagram below shows the four data-driven gameplay elements you’ll create in this part of the tutorial. Once you’ve finished setting up all four elements, you’ll revisit this diagram in more detail to help summarize what you’ve built.

[![](https://dev.epicgames.com/community/api/documentation/image/6109d907-b3d6-41e3-8f34-33676837146c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6109d907-b3d6-41e3-8f34-33676837146c?resizing_type=fit)

First, you’ll create two files to define your item data:

-   `ItemData.h`: A container for the Item Data Struct (`FItemData`) declaration. 
    
-   `ItemDefinition.h`: A class that inherits from `UDataAsset` so your item data can be used in Unreal Editor. 
    

The Item Data Struct doesn’t inherit from `UObject` and can’t be instantiated in a level, so you also need the Data Asset class to use and reference in the editor.

Then, in Unreal Editor, you’ll create a Data Table and a Data Asset Instance based on `ItemDefinition`.

## Define Your Item Data

Your Item Data Struct defines the data or properties each item in the Data Table should have, acting like the table's columns.

Your Item Data Struct will have the following properties:

-   **ID**: A unique name for the item, useful when referencing table rows later.
    
-   **Item Type**: The type of this item (in this case, you’ll define Tool and Consumable types).
    
-   **Item Text**: Textual data about the item, including a name and description.
    
-   **Item Base**: The ItemDefinition Data Asset associated with this item.
    

If you want to create your own table fields (columns), keep in mind that Data Table fields can be any types that are compatible with `UPROPERTY()`.

### Create a Header File Container for the Struct

Set up a new folder and new header (`.h`) file to store your Item Data Struct definition. 

You could create the `FItemData` struct within `ItemDefinition.h`, but putting the struct in a separate file helps organize your data elements and allows for reuse.

To set up a header file as a container for your Item Data Struct, follow these steps:

1.  In Unreal Editor, go to **Tools** \> **New C++ Class**.
    
2.  In the **Choose Parent Class** window, select **None** as the parent class, then click **Next**.
    
3.  Next to **Path**, click the folder icon. In your `Source/*[ProjectName]*` folder, create a new folder named `Data` to store this class.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/23348d29-9f6a-4bdb-b368-ee5bca123810?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/23348d29-9f6a-4bdb-b368-ee5bca123810?resizing_type=fit)
    
4.  Name the class `ItemData` and click **Create Class**.  
    
5.  If Unreal Engine doesn't open your new class files automatically, open your project and `ItemData.h` in Visual Studio.  
    
6.  Delete all text in `ItemData.cpp`, then save and close the file. You won't be using it.
    
7.  In `ItemData.h`, delete everything under the `#include “CoreMinimal.h”` line.   
    
    The `CoreMinimal.h` header includes basic types like `FName`, `FString`, and other types you’ll need to define your data.  
8.  At the top of `ItemData.h`, add `#pragma once` and the following include statements:  
    
    -   `#include “Engine/DataTable.h”`: Required to have your struct inherit from `FTableRowBase`.
        
    -   `#include “ItemData.generated.h”`: Required by Unreal Header Tool. Make sure this include statement comes last for your code to compile properly.
        
    
    C++
    
    `#pragma once  #include "CoreMinimal.h" #include "Engine/DataTable.h" #include "ItemData.generated.h"`
    
    #pragma once #include &quot;CoreMinimal.h&quot; #include &quot;Engine/DataTable.h&quot; #include &quot;ItemData.generated.h&quot;
    
    Copy full snippet(5 lines long)
    
9.  Add a forward declaration for a class named `UItemDefinition`. This will be the Data Asset that you can work with in the editor. 
    
    C++
    
    `class UItemDefinition;`
    
    class UItemDefinition;
    
    Copy full snippet(1 line long)
    

### Define Item Properties

There's no existing variable types for an item type and text data, so you'll need to define these.  

To define an Item Type enum, follow these steps:

1.  Create a new `enum class` that lists all possible item types. In this tutorial, you’ll create Tool and Consumable-type items.  
    
2.  Name the enum class `EItemType` and give it type `uint8`. Add the `UENUM()` macro above it to declare this enum to Unreal Header Tool.  
    
    C++
    
    `// Defines the type of the item. UENUM() enum class EItemType : uint8 { };`
    
    // Defines the type of the item. UENUM() enum class EItemType : uint8 { };
    
    Copy full snippet(5 lines long)
    
3.  Add two custom values to this enum: 
    
    -   `Tool`, adding a `UMETA()` macro with `DisplayName = “Tool”`
        
    -   `Consumable`, adding a `UMETA()` macro with `DisplayName = “Consumable”`
        
    
    C++
    
    `// Defines the type of the item. UENUM() enum class EItemType : uint8 { 	Tool UMETA(DisplayName = "Tool"), 	Consumable UMETA(DisplayName = "Consumable") };`
    
    // Defines the type of the item. UENUM() enum class EItemType : uint8 { Tool UMETA(DisplayName = &quot;Tool&quot;), Consumable UMETA(DisplayName = &quot;Consumable&quot;) };
    
    Copy full snippet(7 lines long)
    

These item types are custom and not built into Unreal Engine; so once you’ve learned the basics, you can make anything you like! (Perhaps a `QuestItem`, `Currency`, or `Disguise`?)  

To define an Item Text struct, follow these steps:

1.  After `EItemType`, create a new struct named `FItemText` with a `USTRUCT()` macro. This struct holds textual data about your item.  
    
    C++
    
    `// Contains textual data about the item. USTRUCT() struct FItemText { };`
    
    // Contains textual data about the item. USTRUCT() struct FItemText { };
    
    Copy full snippet(5 lines long)
    
2.  Inside `FItemText`, add the `GENERATED_BODY()` macro. 
    
3.  Then, add two `FText` properties named `Name` and `Description` to store the name and description for this item. Add the `UPROPERTY()` macro to each with `EditAnywhere` as the arguments.  
    
    C++
    
    ```code
    `// Contains textual data about the item. USTRUCT() struct FItemText { 	GENERATED_BODY()  	// The text name of the item. 	UPROPERTY(EditAnywhere) 	FText Name;`
    
    
    ```
    
    Expand codeCopy full snippet(14 lines long)
    

### Create the Item Data Struct

Now that you’ve added those prerequisite declarations, create the Item Data Struct with your item’s properties inside. These properties become the fields in your Data Table.

Define a struct named `FItemData` that inherits from `FTableRowBase`. Add the `public` specifier to allow it to be visible anywhere and add `GENERATED_BODY()` for Unreal Header Tool.

C++

`// Defines a basic item that can be used in a data table. USTRUCT() struct FItemData : public FTableRowBase { 	GENERATED_BODY() };`

// Defines a basic item that can be used in a data table. USTRUCT() struct FItemData : public FTableRowBase { GENERATED\_BODY() };

Copy full snippet(6 lines long)

`FTableRowBase` is a base struct provided by Unreal Engine that lets you use your custom `USTRUCT`s in a Data Table asset. Unreal uses it to know how to serialize your row struct, to support importing and exporting data from CSV/JSON files, and to ensure type safety when pulling data from the table.

In the `FItemData` struct, add the following declarations:

-   An `FName` named `ID`. Each row in a Data Table needs an associated `FName` to reference.
    
-   An `EItemType enum` named `ItemType`. This is the enum of item types you declared earlier.
    
-   An `FItemText` struct named `ItemText`. This is the struct of text data you declared earlier.
    

Add the `UPROPERTY()` macro to each declaration with `EditAnywhere` and `Category = “Item Data”` arguments.

C++

```code
`// The ID name of this item for referencing in a table row. UPROPERTY(EditAnywhere, Category = "Item Data") FName ID;  // The type of the item. UPROPERTY(EditAnywhere, Category = "Item Data") EItemType ItemType; 	 // Text struct including the item name and description. UPROPERTY(EditAnywhere, Category = "Item Data")`

```

Expand codeCopy full snippet(11 lines long)

Add one more declaration: A `TObjectPtr` to a `UItemDefinition` named `ItemBase`. Give it the same `UPROPERTY` macro as the other properties in the struct.

C++

`// The Data Asset item definition associated with this item. UPROPERTY(EditAnywhere, Category = "Item Data") TObjectPtr<UItemDefinition> ItemBase;`

// The Data Asset item definition associated with this item. UPROPERTY(EditAnywhere, Category = "Item Data") TObjectPtr<UItemDefinition> ItemBase;

Copy full snippet(3 lines long)

`TObjectPtr` is a smart pointer type in Unreal Engine that is a safer way to reference `UObject`\-derived types. It’s an editor-aware, garbage collection-safe replacement for raw `UObject` pointers. It’s a hard reference, so it keeps the object loaded at runtime.

In the next step, you’ll create a `UDataAsset` class named `ItemDefinition`. In your Data Table, you’ll use the `ItemBase` field to reference `ItemDefinition Data Asset` instances. 

Your `FItemData` struct should now look like this:

C++

```code
`// Defines a basic item that can be used in a data table. USTRUCT() struct FItemData : public FTableRowBase { 	GENERATED_BODY()  	// The ID name of this item for referencing in a table row. 	UPROPERTY(EditAnywhere, Category = "Item Data") 	FName ID;`


```

Expand codeCopy full snippet(22 lines long)

Save your code.

## Build a DataAsset Item Definition

So far, you’ve defined your item data, or the type of data that appears in your Data Table. Next, you’ll implement the `UItemDefinition` class you made a forward declaration for in `ItemData.h`. 

This class inherits from `UDataAsset` and therefore is a `UObject`, meaning you can create and use instances of it directly in the editor without going through code. You’ll populate your Data Table with instances of your `UItemDefinition` class. 

To create your `ItemDefinition` DataAsset class (`ItemDefinition.h`), follow these steps:

1.  In Unreal Editor, go to **Tools** \> **New C++ Class**.
    
2.  In the **Choose Parent Class** window, click **All Classes**.
    
3.  Search for and select **DataAsset** as the parent class, then click **Next**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/3d2edb6e-b740-47d1-b407-5ca5636ed963?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3d2edb6e-b740-47d1-b407-5ca5636ed963?resizing_type=fit)
    
4.  Name the class `ItemDefinition` (matching the forward declaration you made in `ItemData.h`), then click **Create Class**.
    

VS should automatically open your new class’ `.h` and `.cpp` files. If not, refresh VS and open the files manually. You’ll just be working in the `.h` file, so you can close the `.cpp` file if desired. 

In `ItemDefinition.h`, add an include for `ItemData.h` because you’ll want to re-use the `ItemType` and `ItemText` properties you declared in that file.

C++

`#include "CoreMinimal.h" #include "Data/ItemData.h" #include "ItemDefinition.generated.h"`

#include "CoreMinimal.h" #include "Data/ItemData.h" #include "ItemDefinition.generated.h"

Copy full snippet(3 lines long)

In `ItemDefinition.h`, in the `UCLASS()` macro above the class definition, add `BlueprintType` and `Blueprintable` specifiers to expose this as a base class for creating Blueprints.

C++

`// Defines a basic item with a static mesh that can be built from the editor. UCLASS(BlueprintType, Blueprintable) class FIRSTPERSON_API UItemDefinition : public UDataAsset { 	GENERATED_BODY() 	 public: 	// Default constructor for the class. 	UItemDefinition(); };`

// Defines a basic item with a static mesh that can be built from the editor. UCLASS(BlueprintType, Blueprintable) class FIRSTPERSON\_API UItemDefinition : public UDataAsset { GENERATED\_BODY() public: // Default constructor for the class. UItemDefinition(); };

Copy full snippet(10 lines long)

In the public section, copy the `FName ID`, `EItemType ItemType`, and `FItemText ItemText` declarations from `ItemData.h`. 

Your item definition gets the same data as the `FItemData` struct so you don’t need to reference the original table when you want to get information about the item.

C++

```code
`public:  	// The ID name of this item for referencing in a table row. 	UPROPERTY(EditAnywhere, Category = "Item Data") 	FName ID;  	// The type of this item. 	UPROPERTY(EditAnywhere, Category = "Item Data") 	EItemType ItemType;`


```

Expand codeCopy full snippet(13 lines long)

After `ItemText`, declare a `TSoftObjectPtr` of type `UStaticMesh` named `WorldMesh`. You’ll use this static mesh to display this item in the world. 

`TSoftObjectPtr` is a special type of weak pointer that acts as a string representation of a path for an asset that only loads when needed. Normally, when declaring a `UObject` pointer property that references an asset, that asset is loaded when the object containing the property is loaded. This could make all assets load when the game starts, causing tremendous overhead and slowdown. `TSoftObjectPtr` is useful for large assets such as meshes that should only load on demand. For more information, see [Asynchronous Asset Loading](https://dev.epicgames.com/documentation/en-us/unreal-engine/asynchronous-asset-loading-in-unreal-engine).   

Add the same `UPROPERTY(EditAnywhere, Category = “Item Data”)` macro to this property.

C++

`// Text struct including the item name and description. UPROPERTY(EditAnywhere, Category = "Item Data") FItemText ItemText;  // The Static Mesh used to display this item in the world. UPROPERTY(EditAnywhere, Category = "Item Data") TSoftObjectPtr<UStaticMesh> WorldMesh;`

// Text struct including the item name and description. UPROPERTY(EditAnywhere, Category = "Item Data") FItemText ItemText; // The Static Mesh used to display this item in the world. UPROPERTY(EditAnywhere, Category = "Item Data") TSoftObjectPtr<UStaticMesh> WorldMesh;

Copy full snippet(7 lines long)

Data Table rows are similar to CSV rows, meant for holding textual data and not storing full assets. To optimize data management, we recommend bundling information like an item’s mesh, material, and animations in a DataAsset as this is the central place where all data about one particular item lives. So, the item’s static mesh property is here in `UItemDefinition` instead of in the `FItemData` struct. 

Your complete `UItemDefinition` class should now look like this:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "Data/ItemData.h" #include "ItemDefinition.generated.h"  /** *	Defines a basic item with a static mesh that can be built from the editor.`

```

Expand codeCopy full snippet(35 lines long)

Save your code and compile it from Visual Studio. 

## Create a Data Asset Instance

With your item data (`FItemData` struct from `ItemData.h`) and item definition (`UItemDefinition` class) defined, you’ve got all the pieces you need to build your item instances and Data Table.

First create a Data Asset for a new projectile pickup item, then create a Data Table and populate it with your Data Asset’s information. 

To create a Data Asset item from your `ItemDefinition` class, follow these steps:

1.  In the **Content Browser**, go to the **Content** \> **FirstPerson** folder, click **Add** or right-click a blank area in the **Asset View**, select **New Folder**, and name it `Data`. 
    
    [![](https://dev.epicgames.com/community/api/documentation/image/99c74d46-a4c9-45eb-991a-2384ff094fd9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/99c74d46-a4c9-45eb-991a-2384ff094fd9?resizing_type=fit)
    
    This is where you’ll store and organize data assets in your game.
    
2.  In the `Data` folder, click **Add** or right-click a blank area in the Asset View and select **Miscellaneous** \> **Data Asset**.
    
    Ensure you pick the Data Asset option with the pie chart icon.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/6bd164ed-1886-4231-a528-c1e9a6a7d895?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6bd164ed-1886-4231-a528-c1e9a6a7d895?resizing_type=fit)
    
3.  In the **Pick Class For Data Asset Instance** window, select **Item Definition** (the C++ class you defined earlier), then click **Select**. Name the new Data Asset `DA_Pickup_001`.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/cf8e6f92-46c9-438d-8914-186286251ad9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cf8e6f92-46c9-438d-8914-186286251ad9?resizing_type=fit)
    
4.  Double-click `DA_Pickup_001` to open it. In its **Details** panel, you’ll see all the properties you defined in `ItemDefinition.h`.
    
5.  Enter `pickup_001` as the **ID**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/c8348f56-08c6-4adc-8f4a-4834cc864da2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c8348f56-08c6-4adc-8f4a-4834cc864da2?resizing_type=fit)
    
6.  Set the **Item Type** to **Consumable**.
    
7.  Expand Item Text and enter any Name and Description.  
    
8.  Set the **World Mesh** to `SM_FoamBullet`.
    
9.  Click **Save** near the top-left corner of the window to save your Data Asset.
    

## Define A Data Table

Now that you have at least one Data Asset to populate a Data Table with, you can create the table! 

Each row in the Data Table is one filled-in instance of your ItemData struct.

To create a Data Table, follow these steps:

1.  In the **Content Browser**, in your `Data` folder, right-click a blank area and select **Miscellaneous** \> **Data Table**.
    
2.  In the **Pick Row Structure** window, select **ItemData** (the `FItemData` struct you defined in `ItemData.h`), then click **OK**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/4b91c7ff-ae80-4d2d-b004-5549142af681?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4b91c7ff-ae80-4d2d-b004-5549142af681?resizing_type=fit)
    
3.  Name the new table `DT_PickupData`, then double-click it to open it.
    

Your Data Table is empty initially. However, you’ll see the properties you defined in `FItemData` as headings at the top of the table, and an additional column named **Row Name**.

To add your pickup item Data Asset as a row in the table, follow these steps:

1.  Click **Add** to add a new row to your table. The DataTable editor lists row entries in the top-left panel in the **Data Table** tab.
    
2.  Double-click the `NewRow` row name and change it to `pickup_001` (the ID of your Data Asset).
    
    You can use any `FName` as the **Row Name**; however, to make it easier to reference the row in code, make the Row Name the same as the Data Asset’s ID.
    
3.  In the **Row Editor** panel, enter the same values you set in the `DA_Pickup_001` Data Asset into the **ID**, **Item Type**, and **Item Text** fields.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/513d67eb-dd98-4458-8501-79fd0eb0db90?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/513d67eb-dd98-4458-8501-79fd0eb0db90?resizing_type=fit)
    
4.  Set the **Item Base** to your `DA_Pickup_001` Data Asset.
    
5.  Save your Data Table.
    

And that’s it! Take a look at the diagram of Data-Driven Gameplay elements you’ve created in this step again and see how they’re all connected:

[![](https://dev.epicgames.com/community/api/documentation/image/3f7ddc65-4c56-406e-9432-2c2a0e9a2dcb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3f7ddc65-4c56-406e-9432-2c2a0e9a2dcb?resizing_type=fit)

You’ve created a Data Table that gets its columns from your `FItemData` struct. You populated the table with a row that contains the data from the Consumable-type `ItemDefinition` Data Asset instance you’ve created and used the `ItemBase` pointer to reference the Data Asset itself. Last, your Data Asset instance got its properties from the parent `UItemDefinition` Data Asset class you created. 

## Next Up

In the next section, you’ll learn how to extend this item definition to create a custom pickup class and instantiate it in your level. 

[

![Create a Respawning Pickup Item](https://dev.epicgames.com/community/api/documentation/image/680d7d74-76be-46e0-9631-a62ac8dd8c04?resizing_type=fit&width=640&height=640)

Create a Respawning Pickup Item

Learn how to use C++ to create custom pickups and initialize them in your level.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/create-a-respawning-pickup-item-in-unreal-engine)

## Complete Code

C++

ItemData.h

```code
`#pragma once  #include "CoreMinimal.h" #include "Engine/DataTable.h" #include "ItemData.generated.h"  class UItemDefinition;  /** *	Defines the type of the item.`

```

Expand codeCopy full snippet(59 lines long)

C++

ItemDefinition.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "Data/ItemData.h" #include "ItemDefinition.generated.h"  /** *	Defines a basic item with a static mesh that can be built from the editor.`

```

Expand codeCopy full snippet(34 lines long)