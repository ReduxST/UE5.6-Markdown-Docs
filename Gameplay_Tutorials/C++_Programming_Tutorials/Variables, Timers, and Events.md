# Variables, Timers, and Events

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-to-variables-timers-and-events-in-unreal-engine-cpp](https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-to-variables-timers-and-events-in-unreal-engine-cpp)  
**Processed:** 2025-06-14 16:45:37

---

This tutorial will show you how to expose variables and functions to the editor, use timers to delay or repeat code execution, and use events to communicate between Actors.

## 1\. Creating an Actor that Uses a Timer

If you are new to **Unreal Engine**, you might want to read our [Programming Quick Start](/documentation/en-us/unreal-engine/unreal-engine-cpp-quick-start) first. For this tutorial, we will assume you are familiar with creating a project and adding C++ code to it.

1.  We will begin by creating a new, Basic Code project, with starter content, named HowTo\_VTE, and then adding an **Actor** class to it. We'll name it Countdown in this tutorial.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b907e5d-ec12-41ad-bd8a-ff6ccef62d73/chooseparentclass.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b637758e-18f1-4807-8ff6-138a436f8aae/nameyouractor.png)
2.  We'll start by creating a simple countdown timer that we can see in-game. In Countdown.h, add the following lines to the end of our class definition:
    
    ```
             `int32 CountdownTime;          UTextRenderComponent* CountdownText;          void UpdateTimerDisplay();`
    		
    Copy full snippet
    ```
    int32 CountdownTime; UTextRenderComponent\* CountdownText; void UpdateTimerDisplay();
3.  In Countdown.cpp, we can create our renderable text **Component** and initialize our countdown time to 3 seconds. We can also turn **Ticking** off for this type of **Actor**, since we will not need it. To do this, we must add the header for the Component at the top of the file, making the "include" section look like this:
    
    ```
            `#include "GameFramework/Actor.h"         #include "Components/TextRenderComponent.h"         #include "Countdown.generated.h"`
    		
    Copy full snippet
    ```
    #include "GameFramework/Actor.h" #include "Components/TextRenderComponent.h" #include "Countdown.generated.h"
    
    With the header included, we can write `ACountdown::ACountdown`. It should look like this:
    
    ```
        `ACountdown::ACountdown()     {         // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = false;         CountdownText = CreateDefaultSubobject<UTextRenderComponent>(TEXT("CountdownNumber"));         CountdownText->SetHorizontalAlignment(EHTA_Center);         CountdownText->SetWorldSize(150.0f);         RootComponent = CountdownText;         CountdownTime = 3;     }`
    
    Copy full snippet
    ```
    ACountdown::ACountdown() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = false; CountdownText = CreateDefaultSubobject<UTextRenderComponent>(TEXT("CountdownNumber")); CountdownText->SetHorizontalAlignment(EHTA\_Center); CountdownText->SetWorldSize(150.0f); RootComponent = CountdownText; CountdownTime = 3; }
4.  `ACountdown::UpdateTimerDisplay` should update our text display to show the time remaining, or zero if the time is up. This code should run when we first spawn our `ACountdown` into the game, and once per second until our `CountdownTime` variable hits zero.
    
    ```
             `void ACountdown::UpdateTimerDisplay()          {              CountdownText->SetText(FString::FromInt(FMath::Max(CountdownTime, 0)));          }`
    		
    Copy full snippet
    ```
    void ACountdown::UpdateTimerDisplay() { CountdownText->SetText(FString::FromInt(FMath::Max(CountdownTime, 0))); }
5.  Whenever we assign a **Timer** to run a function, we are given a **Timer Handle**. We need to hold onto that handle so that we can shut the Timer down when the countdown finishes. Let's add the function to count time down, and the Timer Handle we'll need to control it, to the class definition in `Countdown.h`. While we're there, let's also add a function to do something special when the countdown ends:
    
    ```
             `void AdvanceTimer(); 		          void CountdownHasFinished(); 		          FTimerHandle CountdownTimerHandle;`
    		
    Copy full snippet
    ```
    void AdvanceTimer(); void CountdownHasFinished(); FTimerHandle CountdownTimerHandle;
    
    We can also write the body of `ACountdown::AdvanceTimer` and `ACountdown::CountdownHasFinished` in `Countdown.cpp` now:
    
    ```
         `void ACountdown::AdvanceTimer()      {          --CountdownTime;          UpdateTimerDisplay();          if (CountdownTime < 1)          {              //We're done counting down, so stop running the timer.              GetWorldTimerManager().ClearTimer(CountdownTimerHandle);              CountdownHasFinished();          }      }       void ACountdown::CountdownHasFinished()      {          //Change to a special readout          CountdownText->SetText(TEXT("GO!"));      }`
    
    Copy full snippet
    ```
    void ACountdown::AdvanceTimer() { --CountdownTime; UpdateTimerDisplay(); if (CountdownTime < 1) { //We're done counting down, so stop running the timer. GetWorldTimerManager().ClearTimer(CountdownTimerHandle); CountdownHasFinished(); } } void ACountdown::CountdownHasFinished() { //Change to a special readout CountdownText->SetText(TEXT("GO!")); }
6.  Let's initialize the text display in `ACountdown::BeginPlay` by adding a call to our new update function, and setting a timer to advance and update the countdown once per second:
    
    ```
             `UpdateTimerDisplay();          GetWorldTimerManager().SetTimer(CountdownTimerHandle, this, &ACountdown::AdvanceTimer, 1.0f, true);`
    		
    Copy full snippet
    ```
    UpdateTimerDisplay(); GetWorldTimerManager().SetTimer(CountdownTimerHandle, this, &ACountdown::AdvanceTimer, 1.0f, true);
    
    We are updating the display in `ACountdown::BeginPlay` rather than `ACountdown::ACountdown` because values set to variables in the Unreal Editor will be assigned after the constructor, but before **BeginPlay**. We will want to respect those values later, when we expose `CountdownTime` to the editor.
    
7.  Let's check our progress so far by going to the **Unreal Editor** and pressing **Compile**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c98dfe59-e499-437c-b7f5-f2bd94d49cb2/compilefromeditor.png)
    
    We can then drop our updated `ACountdown` class from the **Content Browser** into the **Level Editor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b55f02a6-64d7-42f1-9d3f-a90af19cb301/classincontentbrowser.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb05729a-e396-484d-9551-c0bb4e19116a/leveleditortext.png)
    
    Because we set our countdown text during `ACountdown::BeginPlay` and not `ACountdown::ACountdown`, the default Text is shown in the **Level Editor**.
    
    When we press **Play**, the countdown will progress as expected, saying 3, 2, 1, and finally GO!
    

At this point, we've already created a simple class that uses a timer. Non-programming users would get much more out of it if they could set the countdown time, or change the behavior when the countdown finishes. Next, we'll expose these features to the editor.

### Work-In-Progress Code

**Countdown.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "GameFramework/Actor.h" 	#include "Countdown.generated.h"  	UCLASS() 	class HOWTO_VTE_API ACountdown : public AActor 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this actor's properties 		ACountdown();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick( float DeltaSeconds ) override;  		//How long, in seconds, the countdown will run 		int32 CountdownTime;  		UTextRenderComponent* CountdownText;  		void UpdateTimerDisplay();  		void AdvanceTimer();  		void CountdownHasFinished();  		FTimerHandle CountdownTimerHandle; 	};`
Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "GameFramework/Actor.h" #include "Countdown.generated.h" UCLASS() class HOWTO\_VTE\_API ACountdown : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties ACountdown(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaSeconds ) override; //How long, in seconds, the countdown will run int32 CountdownTime; UTextRenderComponent\* CountdownText; void UpdateTimerDisplay(); void AdvanceTimer(); void CountdownHasFinished(); FTimerHandle CountdownTimerHandle; };

**Countdown.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "HowTo_VTE.h" 	#include "Components/TextRenderComponent.h" 	#include "Countdown.h"  	// Sets default values 	ACountdown::ACountdown() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = false;  		CountdownText = CreateDefaultSubobject<UTextRenderComponent>(TEXT("CountdownNumber")); 		CountdownText->SetHorizontalAlignment(EHTA_Center); 		CountdownText->SetWorldSize(150.0f); 		RootComponent = CountdownText;  		CountdownTime = 3; 	}  	// Called when the game starts or when spawned 	void ACountdown::BeginPlay() 	{ 		Super::BeginPlay();  		UpdateTimerDisplay(); 		GetWorldTimerManager().SetTimer(CountdownTimerHandle, this, &ACountdown::AdvanceTimer, 1.0f, true); 	}  	// Called every frame 	void ACountdown::Tick( float DeltaTime ) 	{ 		Super::Tick( DeltaTime );  	}  	void ACountdown::UpdateTimerDisplay() 	{ 		CountdownText->SetText(FString::FromInt(FMath::Max(CountdownTime, 0))); 	}  	void ACountdown::AdvanceTimer() 	{ 		--CountdownTime; 		UpdateTimerDisplay(); 		if (CountdownTime < 1) 		{ 			// We're done counting down, so stop running the timer. 			GetWorldTimerManager().ClearTimer(CountdownTimerHandle); 			//Perform any special actions we want to do when the timer ends. 			CountdownHasFinished(); 		} 	}  	void ACountdown::CountdownHasFinished() 	{ 		//Change to a special readout 		CountdownText->SetText(TEXT("GO!")); 	}`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "HowTo\_VTE.h" #include "Components/TextRenderComponent.h" #include "Countdown.h" // Sets default values ACountdown::ACountdown() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = false; CountdownText = CreateDefaultSubobject<UTextRenderComponent>(TEXT("CountdownNumber")); CountdownText->SetHorizontalAlignment(EHTA\_Center); CountdownText->SetWorldSize(150.0f); RootComponent = CountdownText; CountdownTime = 3; } // Called when the game starts or when spawned void ACountdown::BeginPlay() { Super::BeginPlay(); UpdateTimerDisplay(); GetWorldTimerManager().SetTimer(CountdownTimerHandle, this, &ACountdown::AdvanceTimer, 1.0f, true); } // Called every frame void ACountdown::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } void ACountdown::UpdateTimerDisplay() { CountdownText->SetText(FString::FromInt(FMath::Max(CountdownTime, 0))); } void ACountdown::AdvanceTimer() { --CountdownTime; UpdateTimerDisplay(); if (CountdownTime < 1) { // We're done counting down, so stop running the timer. GetWorldTimerManager().ClearTimer(CountdownTimerHandle); //Perform any special actions we want to do when the timer ends. CountdownHasFinished(); } } void ACountdown::CountdownHasFinished() { //Change to a special readout CountdownText->SetText(TEXT("GO!")); }

## 2\. Exposing Variables and Functions to the Editor

1.  Our countdown timer is currently hard-coded to use a value of 3 seconds. It would be more useful if we could set the countdown time to any value we want in the editor, and this is easy to do. In **Visual Studio**, we can open `Countdown.h` and find the line that says:
    
    ```
             `int32 CountdownTime;`
    		
    Copy full snippet
    ```
    int32 CountdownTime;
    
    In order to expose this variable to Unreal Engine, we need to make it a `UPROPERTY`. This enables the engine to preserve the value of the variable when launching the game or loading a saved level. The `UPROPERTY` tag, with empty parentheses, is added right above the variable it affects:
    
    ```
         `UPROPERTY()      int32 CountdownTime;`
    
    Copy full snippet
    ```
    UPROPERTY() int32 CountdownTime;
    
    `UPROPERTY` supports arguments that change how Unreal Engine will use the variable. Since we want our variable to be editable, we can add the `EditAnywhere` argument:
    
    ```
         `UPROPERTY(EditAnywhere)      int32 CountdownTime;`
    
    Copy full snippet
    ```
    UPROPERTY(EditAnywhere) int32 CountdownTime; ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a9d1bb6-2940-4351-9599-0c0c24a098af/exposingvariable.png)
    
    We can also add a comment to our variable in C++, and our comment will become the description of the variable in the Unreal Editor, like this:
    
    ```
         `//How long, in seconds, the countdown will run      UPROPERTY(EditAnywhere)      int32 CountdownTime;`
    
    Copy full snippet
    ```
    //How long, in seconds, the countdown will run UPROPERTY(EditAnywhere) int32 CountdownTime; ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06bdb07d-d281-4331-90dc-dcbc66b4a1b4/commentingvariable.png)
    
    There is a lot more we can do with `UPROPERTY`, and looking into other Specifiers such as `BlueprintReadWrite` and `Category` might be good next steps, but we have all that we need at the moment.
    
    When we return to the Unreal Editor and press **Compile**, our variable will appear in the **Details Panel** for the `ACountdown` we placed earlier, and we can test out different timer values by changing this number and pressing **Play**.
    
2.  In addition to changing the value of the timer, let's also enable non-programming developers to change what happens when the timer is up. In Visual Studio, we'll open Countdown.h and find the following line:
    
    ```
             `void CountdownHasFinished();`
    		
    Copy full snippet
    ```
    void CountdownHasFinished();
    
    We can expose this function to the Unreal Engine by making it a `UFUNCTION`, like this:
    
    ```
         `UFUNCTION()      void CountdownHasFinished();`
    
    Copy full snippet
    ```
    UFUNCTION() void CountdownHasFinished();
    
    Just like the `UPROPERTY` macro, we need to provide information about what can be done with it in order to enable more features and access for non-programming developers. There are three options to consider:
    
    1.  `BlueprintCallable` functions are written in C++ and can be called from the **Blueprint Graph**, but cannot be changed or overridden without editing C++ code. Functions marked this way are usually features that have been programmed for non-programmer use, but that are not supposed to be changed or wouldn't make sense to change. An easy example of this would be any kind of math function.
        
    2.  `BlueprintImplementableEvent` functions are set up in a C++ header (.h) file, but the body of the function is written entirely in the Blueprint Graph, not in C++. These are usually created to give a non-programmer the ability to create custom reactions to special situations that have no expected default action or standard behavior. An example of this might be an event that happens when a powerup touches the player's ship in a spaceship game.
        
    3.  `BlueprintNativeEvent` functions are like a combination of `BlueprintCallable` and `BlueprintImplementableEvent` functions. They have default behaviors programmed in C++, but these can be supplemented or replaced by overriding in the Blueprint Graph. When programming these, the C++ code always goes in a virtual function with \_Implementation added to the end of the name, as shown below. This is the most flexible option, so we will use it for this tutorial.
        
    
    To grant non-programmers the ability to call our C++ function and to override it with **Blueprints**, we need to make the following changes to `Countdown.h`:
    
    ```
         `UFUNCTION(BlueprintNativeEvent)      void CountdownHasFinished();      virtual void CountdownHasFinished_Implementation();`
    
    Copy full snippet
    ```
    UFUNCTION(BlueprintNativeEvent) void CountdownHasFinished(); virtual void CountdownHasFinished\_Implementation();
    
    Then, in Countdown.cpp, we will need to change the line that says:
    
    ```
         `void ACountdown::CountdownHasFinished()`
    
    Copy full snippet
    ```
    void ACountdown::CountdownHasFinished()
    
    To:
    
    ```
         `void ACountdown::CountdownHasFinished_Implementation()`
    Copy full snippet
    ```
    void ACountdown::CountdownHasFinished\_Implementation()

We have now made a variable and a function accessible to, and alterable by, non-programmers, while providing our own default value and functionality in C++. To see how a non-programmer might use this, we'll make a Blueprint extension of our `ACountdown` class and modify it ourselves.

### Finished Code

**Countdown.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "GameFramework/Actor.h" 	#include "Countdown.generated.h"  	UCLASS() 	class HOWTO_VTE_API ACountdown : public AActor 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this actor's properties 		ACountdown();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick( float DeltaSeconds ) override;  		//How long, in seconds, the countdown will run 		UPROPERTY(EditAnywhere) 		int32 CountdownTime;  		UTextRenderComponent* CountdownText;  		void UpdateTimerDisplay();  		void AdvanceTimer();  		UFUNCTION(BlueprintNativeEvent) 		void CountdownHasFinished(); 		virtual void CountdownHasFinished_Implementation();  		FTimerHandle CountdownTimerHandle; 	};`
Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "GameFramework/Actor.h" #include "Countdown.generated.h" UCLASS() class HOWTO\_VTE\_API ACountdown : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties ACountdown(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaSeconds ) override; //How long, in seconds, the countdown will run UPROPERTY(EditAnywhere) int32 CountdownTime; UTextRenderComponent\* CountdownText; void UpdateTimerDisplay(); void AdvanceTimer(); UFUNCTION(BlueprintNativeEvent) void CountdownHasFinished(); virtual void CountdownHasFinished\_Implementation(); FTimerHandle CountdownTimerHandle; };

**Countdown.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "HowTo_VTE.h" 	#include "Components/TextRenderComponent.h" 	#include "Countdown.h"  	// Sets default values 	ACountdown::ACountdown() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = false;  		CountdownText = CreateDefaultSubobject<UTextRenderComponent>(TEXT("CountdownNumber")); 		CountdownText->SetHorizontalAlignment(EHTA_Center); 		CountdownText->SetWorldSize(150.0f); 		RootComponent = CountdownText;  		CountdownTime = 3; 	}  	// Called when the game starts or when spawned 	void ACountdown::BeginPlay() 	{ 		Super::BeginPlay();  		UpdateTimerDisplay(); 		GetWorldTimerManager().SetTimer(CountdownTimerHandle, this, &ACountdown::AdvanceTimer, 1.0f, true); 	}  	// Called every frame 	void ACountdown::Tick( float DeltaTime ) 	{ 		Super::Tick( DeltaTime );  	}  	void ACountdown::UpdateTimerDisplay() 	{ 		CountdownText->SetText(FString::FromInt(FMath::Max(CountdownTime, 0))); 	}  	void ACountdown::AdvanceTimer() 	{ 		--CountdownTime; 		UpdateTimerDisplay(); 		if (CountdownTime < 1) 		{ 			// We're done counting down, so stop running the timer. 			GetWorldTimerManager().ClearTimer(CountdownTimerHandle); 			//Perform any special actions we want to do when the timer ends. 			CountdownHasFinished(); 		} 	}  	void ACountdown::CountdownHasFinished_Implementation() 	{ 		//Change to a special readout 		CountdownText->SetText(TEXT("GO!")); 	}`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "HowTo\_VTE.h" #include "Components/TextRenderComponent.h" #include "Countdown.h" // Sets default values ACountdown::ACountdown() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = false; CountdownText = CreateDefaultSubobject<UTextRenderComponent>(TEXT("CountdownNumber")); CountdownText->SetHorizontalAlignment(EHTA\_Center); CountdownText->SetWorldSize(150.0f); RootComponent = CountdownText; CountdownTime = 3; } // Called when the game starts or when spawned void ACountdown::BeginPlay() { Super::BeginPlay(); UpdateTimerDisplay(); GetWorldTimerManager().SetTimer(CountdownTimerHandle, this, &ACountdown::AdvanceTimer, 1.0f, true); } // Called every frame void ACountdown::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } void ACountdown::UpdateTimerDisplay() { CountdownText->SetText(FString::FromInt(FMath::Max(CountdownTime, 0))); } void ACountdown::AdvanceTimer() { --CountdownTime; UpdateTimerDisplay(); if (CountdownTime < 1) { // We're done counting down, so stop running the timer. GetWorldTimerManager().ClearTimer(CountdownTimerHandle); //Perform any special actions we want to do when the timer ends. CountdownHasFinished(); } } void ACountdown::CountdownHasFinished\_Implementation() { //Change to a special readout CountdownText->SetText(TEXT("GO!")); }

## 3\. Extend and Override C++ with Blueprints

This section of the tutorial involves using **Blueprints** to extend the functionality of C++ classes. However, it is only intended as a test that our C++ code was written correctly, not as a Blueprint tutorial. For a proper introduction to Blueprints, we recommend the [%programming-and-scripting/blueprints-visual-scripting/GettingStarted/QuickStart:title%](/documentation/en-us/unreal-engine/quick-start-guide-for-blueprints-visual-scripting-in-unreal-engine).

1.  To change the behavior of our ACountdown instance, called Countdown1, in the editor, we must first make an editable Blueprint version of it. To do this, we can select it from the **World Outliner** and click the **Blueprint/Add Script** button in the **Details Panel**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77e1129d-8183-468d-9f14-adfdab59664a/addscript.png)
    
    From there, we can provide a path and name for the Blueprint asset that will contain our modified ACountdown class.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9eeb1139-cbeb-4405-b7de-b54f63eb9fce/selectblueprintpath.png)
    
    This will create a new asset that represents a Blueprint version of Countdown1. It will also replace Countdown1 with an instance of this new Blueprint, so that changes we make to the Blueprint will affect Countdown1 in the game.
    
2.  The **Unreal Editor** will automatically take us to our new asset in the **Content Browser**, and we can **Right-click** it and choose "Edit..." to modify its **Blueprint Graph**, **Component** hierarchy, and **Default Values**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e2e3df9-7008-4766-a6aa-359e5f6f611e/blueprintincontentbrowser.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7da68bfa-e0a6-4f5c-89bf-af0e99ce1f5e/editblueprint.png)
3.  Functions and events can be found in the **Event Graph** tab, so we'll select that first.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe43a413-25e6-46e8-9e45-88e4b165fc12/selecteventgraph.png)
    
    Then, by **Right-clicking** anywhere in the **Event Graph** window, we can add our **CountdownHasFinished** function as an event node to define its behavior.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e297b10-c767-450c-8125-6b87a3376366/selectevent.png)
4.  We can now add any additional functionality we would like by left-clicking and dragging off of the white (execution) pin on the right side of our new node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fd5484e-1d51-4b9c-9808-2fd3391ac5f0/dragexecpin.png)
    
    When we release the left mouse button, we will be asked what function or event we would like to execute. For this tutorial, let's spawn a **Particle System** when the countdown finishes. We'll want a **Spawn Emitter At Location** node, so select that from the list. It can save time to type a partial phrase, like spawn loc, into the search field. We can then left-click and drag the yellow "Location" pin and attach it to a **Get Actor Location** function.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59762911-ae9e-4c91-a6c0-6ce26a84b74b/getactorlocation.png)
    
    Now we just need to select what effect we'd like to see. By clicking Select Asset under Emitter Template, we can get a list of appropriate effect assets. P\_Explosion is a good one, so we'll pick that.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/858a4022-2a8b-4bc1-97a7-4f06b451665d/selectparticle.png)
5.  Click the **Compile** button at the top left of the **Blueprint Editor** to save the changes.
    
6.  If we press **Play** now, we'll see our countdown take place, and our explosion will happen when our countdown number hits zero.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91002fda-5715-4fbf-b9bb-b67d5d069545/explosion_zero.png)
    
    However, we programmed our countdown to say GO! at the end, not 0. This is no longer happening because we have completely replaced our C++ functionality with our **Blueprint** visual scripting. This is not what we intended to do in this case, so we need to add a call to the C++ version of this function, which can be done by right-clicking the **Countdown Has Finished** node and selecting **Add call to parent function** from the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90e15ad7-255d-43f8-ad0d-6e86e456a589/calltoparent_menu.png)
    
    When this is done, a node labeled **Parent: Countdown Has Finished** will be placed in the **Event Graph**. The typical place to connect a parent node is directly to the event node, which is what we will do here. This is not required, though, as the parent-call node is like any other and can be called anywhere we like, even multiple times.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13ad81c7-707f-4072-a7c5-575b49fd5693/calltoparent_connectpins.png)
    
    Note that this will replace the connection to **Spawn Emitter At Location**, so we'll need to connect our \*\*Parent: programming-and-scripting/programming-language-implementation/cpp-in-unreal-engine/unreal-engine-cpp-tutorials
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c78b8ea-6a5c-4918-9518-d01e351a587b/calltoparent_fixpins.png)
    
    Now when we run our game, we should see both the word GO! (from our C++ code) and an explosion (from our Blueprint Graph) after the countdown finishes!
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f82a8abf-413c-432e-9305-a1f8576da0af/explosion_go.png)

## 4\. On Your Own!

Using what you have learned, try to do the following:

-   Create an **Actor** that moves or rotates to a target transform when an **Event** is run. This could be used as a moving platform or door in a game. Make the Event start a **Timer** that will trigger a second Event which moves the Actor back to its original location. Use exposed variables (that is, exposed through `UPROPERTY`) instead of hard-coded values wherever appropriate.
-   Make a lit torch that burns out (perhaps by deactivating a fiery **Particle System Component**) by using a Timer handle and a few custom Events. For example, an AddFuel Event could extend the burning time of the torch. A DouseWithWater Event could shut it off immediately and prevent AddFuel from working in the future. Both of these features can be written without using a **Tick**, simply by modifying a running Timer through its handle.

As for the specifics covered in this tutorial:

-   For more information about Timers, try the [Gameplay Timers](/documentation/en-us/unreal-engine/gameplay-timers-in-unreal-engine) page.
-   For a complete reference using the `UPROPERTY` tag with variables in your classes or structs, look at the [%programming-and-scripting/programming-language-implementation/unreal-engine-reflection-system/Properties:title%](/documentation/en-us/unreal-engine/unreal-engine-uproperties) page.
-   To learn more about `UFUNCTIONS` and Event creation, check the [%programming-and-scripting/programming-language-implementation/unreal-engine-reflection-system/Functions:title%](/documentation/en-us/unreal-engine/ufunctions-in-unreal-engine) page.
-   For further tutorials, see the [%programming-and-scripting/programming-language-implementation/cpp-in-unreal-engine/tutorials:title%](/documentation/en-us/unreal-engine/unreal-engine-cpp-programming-tutorials) page.