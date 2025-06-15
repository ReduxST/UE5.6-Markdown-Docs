# Gameplay Debugger

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-gameplay-debugger-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-gameplay-debugger-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:28

---

The **Gameplay Debugger Tool (GDT)** is useful for watching real-time data at runtime, even on clients in networked games using replication. It works in **Play In Editor (PIE)**, **Simulate In Editor (SIE)**, and standalone game sessions, and all of the data is displayed as an overlay on the game viewport. The system provides a framework that can be extended to enable debugging of game-specific data.

**Unreal Engine** implementation can show:

-   Basic data from Pawn
-   Basic data from AIController
-   Information about Behavior Tree and Blackboard data
-   Information about executed Environment Queries (EQS)
-   Information from perception system
-   Navmesh around player or selected Pawn with all details like links or areas

Usually there is a lot of data so GDT use categories to limit amount of information on screen. Data from only enabled categories is replicated which saves replication channel's bandwidth. There are 5 default categories and 5 categories to use by projects:

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a04b9483-4d62-4769-94a0-6c028933ae51/image_1.png)

-   Navmesh
-   Basic
-   Behavior Tree
-   EQS
-   Perception
-   and 5 categories to use by projects

Existing categories can be extended to show more game-specific data too.

Below we have screen-shots captured on a client with a few enabled categories: **Basic**, **EQS**, **NavMesh** and **Behavior Tree**.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3faf75d-96e8-4eaf-ba13-4a4b3557aa62/image_2.png)

Gameplay Debugger can be activated with the **apostrophe (')** key by default or with `EnableGDT` cheat. Key binding is set in file and can be easily changed. To select an enemy for debugging press the apostrophe (') key while pointing to that enemy onscreen. Use the numeric keyboard to switch between visible categories. The GameplayDebugger module has to be added to project's dependency modules to be activated and usable.

## Working with Gameplay Debugger

While working in the Editor, GDT can be used in PIE or in Simulate. A bound key or the `EnableGDT` cheat can be used to activate GDT in PIE. Simulate mode is little different from PIE; to activate this debug tool in Simulate you need to enable the `Debug AI` show flag. There is an option to change visible categories in Simulate too. The **GameplayDebuggingReplicator** Actor is used for that. This Actor can be found in the Scene Outliner, and this Actor's properties are used to control GDT.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e358c32a-04a2-415e-b5cc-ede4a3244d09/image_3.jpg)

## Debug Camera Controller

The DebugCameraController also has the following features:

-   **Orbit** functionality - this allows you to orbit the camera around a selected position, or the center of a selected Actor, so you can review assets more thoroughly.
-   **Buffer visualization overview** - this gives you an option to select buffers for fullscreen view, and makes it possible to examine the contents of the graphic card buffers.
-   **View mode cycling** - this gives you the ability to examine the different types of scene data being processed.

The new features augment in-game debugging capabilities when you are using the Debug Camera Controller in Play-In-Editor (PIE). The ability to examine view modes and graphics buffers helps you diagnose unexpected scene results in-game.

To open the debug camera controller in PIE, enter `ToggleDebugCamera` on the console command line, or use the **semicolon (;)** hotkey.

## Basic extension

Gameplay Debugger can be only extended with C++ code. For Blueprint projects it can only be used as-is to display basic debug information. It is easy to extend the Gameplay Debugger to collect and display game-specific data. To accomplish this, you need custom classes inherited from the `UGameplayDebuggingComponent` class and the `AGameplayDebuggingHUDComponent` class. The first class is used to collect and eventually replicate the data, and the second class is used to display all the collected data onscreen.

Below is a simple class which collects game specific data:

```
	`GDTComponent.h  	// Copyright Epic Games, Inc. All Rights Reserved. 	#pragma once 	#include "GameplayDebuggingComponent.h" 	#include "GDTComponent.generated.h"  	UCLASS() 	class UGDTComponent : public UGameplayDebuggingComponent 	{ 	public: 		GENERATED_UCLASS_BODY() 		virtual void CollectBasicData() override;  		UPROPERTY(Replicated) 		float TestData; //custom data replicated to clients 	};  	GDTComponent.cpp  	// Copyright Epic Games, Inc. All Rights Reserved. 	#include "MyGameProject.h" 	#include "GameplayDebuggingComponent.h" 	#include "GDTComponent.h"  	UGDTComponent::UGDTComponent(const class FPostConstructInitializeProperties& PCIP) : Super(PCIP) { }  	void UGDTComponent::GetLifetimeReplicatedProps(TArray<FLifetimeProperty> &OutLifetimeProps) const 	{ 		Super::GetLifetimeReplicatedProps( OutLifetimeProps ); 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		DOREPLIFETIME( UGDTComponent, TestData); 	#endif 	}  	void UGDTComponent::CollectBasicData() 	{ 		Super::CollectBasicData(); 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		TestData= FMath::RandRange(2.75, 8.25); //collect data and store it 	#endif 	}`

Copy full snippet
```
GDTComponent.h // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "GameplayDebuggingComponent.h" #include "GDTComponent.generated.h" UCLASS() class UGDTComponent : public UGameplayDebuggingComponent { public: GENERATED\_UCLASS\_BODY() virtual void CollectBasicData() override; UPROPERTY(Replicated) float TestData; //custom data replicated to clients }; GDTComponent.cpp // Copyright Epic Games, Inc. All Rights Reserved. #include "MyGameProject.h" #include "GameplayDebuggingComponent.h" #include "GDTComponent.h" UGDTComponent::UGDTComponent(const class FPostConstructInitializeProperties& PCIP) : Super(PCIP) { } void UGDTComponent::GetLifetimeReplicatedProps(TArray<FLifetimeProperty> &OutLifetimeProps) const { Super::GetLifetimeReplicatedProps( OutLifetimeProps ); #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) DOREPLIFETIME( UGDTComponent, TestData); #endif } void UGDTComponent::CollectBasicData() { Super::CollectBasicData(); #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) TestData= FMath::RandRange(2.75, 8.25); //collect data and store it #endif }

The next class is used to display new data on screen:

```
	`GDTHUDComponent.h  	// Copyright Epic Games, Inc. All Rights Reserved. 	#pragma once  	#include "GameplayDebuggingHUDComponent.h" 	#include "GDTHUDComponent.generated.h"  	UCLASS(notplaceable) 	class AGDTHUDComponent: public AGameplayDebuggingHUDComponent 	{ 		GENERATED_UCLASS_BODY() 	protected: 		virtual void DrawBasicData(APlayerController* PC, class UGameplayDebuggingComponent *DebugComponent) override; 	};  	GDTHUDComponent.cpp  	// Copyright Epic Games, Inc. All Rights Reserved. 	#include "MyGameProject.h" 	#include "GDTComponent.h" 	#include "GDTHUDComponent.h"  	AGDTHUDComponent::AGDTHUDComponent(const class FPostConstructInitializeProperties& PCIP) 		: Super(PCIP) 	{ 	} 	void AGDTHUDComponent::DrawBasicData(APlayerController* PC, class UGameplayDebuggingComponent *DebugComponent) 	{ 		Super::DrawBasicData(PC, DebugComponent); 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		const UGDTComponent* MyComp = Cast<UGDTComponent>(DebugComponent); 		if (MyComp) 		{ 			PrintString(DefaultContext, FString::Printf(TEXT("{white}Test data: {red}%f\n"), MyComp->TestData)); 		} 	#endif 	}`

Copy full snippet
```
GDTHUDComponent.h // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "GameplayDebuggingHUDComponent.h" #include "GDTHUDComponent.generated.h" UCLASS(notplaceable) class AGDTHUDComponent: public AGameplayDebuggingHUDComponent { GENERATED\_UCLASS\_BODY() protected: virtual void DrawBasicData(APlayerController\* PC, class UGameplayDebuggingComponent \*DebugComponent) override; }; GDTHUDComponent.cpp // Copyright Epic Games, Inc. All Rights Reserved. #include "MyGameProject.h" #include "GDTComponent.h" #include "GDTHUDComponent.h" AGDTHUDComponent::AGDTHUDComponent(const class FPostConstructInitializeProperties& PCIP) : Super(PCIP) { } void AGDTHUDComponent::DrawBasicData(APlayerController\* PC, class UGameplayDebuggingComponent \*DebugComponent) { Super::DrawBasicData(PC, DebugComponent); #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) const UGDTComponent\* MyComp = Cast<UGDTComponent>(DebugComponent); if (MyComp) { PrintString(DefaultContext, FString::Printf(TEXT("{white}Test data: {red}%f\\n"), MyComp->TestData)); } #endif }

The Gameplay Debugger needs to know about new classes, and that information can be set in the `DefaultEngine.ini` configuration file.

```
	`DefaultEngine.ini  	[/Script/GameplayDebugger.GameplayDebuggingReplicator] 	DebugComponentClassName="/Script/MyGameProject.GDTComponent" 	DebugComponentHUDClassName="/Script/MyGameProject.GDTHUDComponent" |`

Copy full snippet
```
DefaultEngine.ini \[/Script/GameplayDebugger.GameplayDebuggingReplicator\] DebugComponentClassName="/Script/MyGameProject.GDTComponent" DebugComponentHUDClassName="/Script/MyGameProject.GDTHUDComponent" |

## Custom categories

A few more steps are needed to add a project-specific category to the Gameplay Debugger.

Let's extend the `GDTComponent` class.

```
	`GDTComponent.h  	// Copyright Epic Games, Inc. All Rights Reserved. 	#pragma once 	#include "GameplayDebuggingComponent.h" 	#include "GDTComponent.generated.h"  	UCLASS() 	class UGDTComponent : public UGameplayDebuggingComponent 	{ 	public: 		GENERATED_UCLASS_BODY() 	protected: 		virtual void CollectDataToReplicate(bool bCollectExtendedData) override; 		void CollectCustomData(); 	public: 		UPROPERTY(Replicated) 		float TestData; //custom data replicated to clients 	};  	GDTComponent.cpp  	// Copyright Epic Games, Inc. All Rights Reserved. 	#include "MyGameProject.h" 	#include "GameplayDebuggingComponent.h" 	#include "GDTComponent.h"  	UGDTComponent::UGDTComponent(const class FPostConstructInitializeProperties& PCIP) : Super(PCIP) { }  	void UGDTComponent::GetLifetimeReplicatedProps(TArray<FLifetimeProperty> &OutLifetimeProps) const 	{ 		Super::GetLifetimeReplicatedProps( OutLifetimeProps ); 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		DOREPLIFETIME( UGDTComponent, TestData); 	#endif 	}  	void UGDTComponent::CollectCustomData() 	{ 		Super::CollectBasicData(); 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		TestData= FMath::RandRange(2.75, 8.25); //collect data and store it 	#endif 	}  	void UGDTComponent::CollectDataToReplicate(bool bCollectExtendedData) 	{ 		Super::CollectDataToReplicate(bCollectExtendedData); 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		if (ShouldReplicateData(EAIDebugDrawDataView::GameView1)) 		{ 			CollectCustomData(); 			if (bCollectExtendedData) 			{ 				// collect additional data for selected Pawn/AIController 			} 		} 	#endif 	}`

Copy full snippet
```
GDTComponent.h // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "GameplayDebuggingComponent.h" #include "GDTComponent.generated.h" UCLASS() class UGDTComponent : public UGameplayDebuggingComponent { public: GENERATED\_UCLASS\_BODY() protected: virtual void CollectDataToReplicate(bool bCollectExtendedData) override; void CollectCustomData(); public: UPROPERTY(Replicated) float TestData; //custom data replicated to clients }; GDTComponent.cpp // Copyright Epic Games, Inc. All Rights Reserved. #include "MyGameProject.h" #include "GameplayDebuggingComponent.h" #include "GDTComponent.h" UGDTComponent::UGDTComponent(const class FPostConstructInitializeProperties& PCIP) : Super(PCIP) { } void UGDTComponent::GetLifetimeReplicatedProps(TArray<FLifetimeProperty> &OutLifetimeProps) const { Super::GetLifetimeReplicatedProps( OutLifetimeProps ); #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) DOREPLIFETIME( UGDTComponent, TestData); #endif } void UGDTComponent::CollectCustomData() { Super::CollectBasicData(); #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) TestData= FMath::RandRange(2.75, 8.25); //collect data and store it #endif } void UGDTComponent::CollectDataToReplicate(bool bCollectExtendedData) { Super::CollectDataToReplicate(bCollectExtendedData); #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) if (ShouldReplicateData(EAIDebugDrawDataView::GameView1)) { CollectCustomData(); if (bCollectExtendedData) { // collect additional data for selected Pawn/AIController } } #endif }

Here we extend the HUD component, to display data in a new view.

```
	`GDTHUDComponent.h  	// Copyright Epic Games, Inc. All Rights Reserved. 	#pragma once  	#include "GameplayDebuggingHUDComponent.h" 	#include "GDTHUDComponent.generated.h"  	UCLASS(notplaceable) 	class AGDTHUDComponent: public AGameplayDebuggingHUDComponent 	{ 		GENERATED_UCLASS_BODY() 	protected: 		virtual void DrawGameSpecificView(APlayerController* PC, class UGameplayDebuggingComponent *DebugComponent) override; 		virtual void GetKeyboardDesc(TArray<FDebugCategoryView>& Categories) override; 		void DrawCustomData(APlayerController* PC, class UGameplayDebuggingComponent *DebugComponent); 	};  	GDTHUDComponent.cpp  	// Copyright Epic Games, Inc. All Rights Reserved. 	#include "MyGameProject.h" 	#include "GDTComponent.h" 	#include "GDTHUDComponent.h"  	AGDTHUDComponent::AGDTHUDComponent(const class FPostConstructInitializeProperties& PCIP) 		: Super(PCIP) 	{ 	} 	void AGDTHUDComponent::DrawCustomData(APlayerController* PC, class UGameplayDebuggingComponent *DebugComponent) 	{ 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		const UGDTComponent* MyComp = Cast<UGDTComponent>(DebugComponent); 		if (MyComp) 		{ 			PrintString(DefaultContext, FString::Printf(TEXT("{white}Test data: {red}%f\n"), MyComp->TestData)); 		} 	#endif 	} 	void AGDTHUDComponent::GetKeyboardDesc(TArray<FDebugCategoryView>& Categories) 	{ 		Super::GetKeyboardDesc(Categories); 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		Categories.Add(FDebugCategoryView(EAIDebugDrawDataView::GameView1, TEXT("MyData"))); 	#endif 	} 	void AGDTHUDComponent::DrawGameSpecificView(APlayerController* PC, class UGameplayDebuggingComponent *InDebugComponent) 	{ 		 Super::DrawGameSpecificView(PC, InDebugComponent); 	#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) 		if (InDebugComponent && GameplayDebuggerSettings(GetDebuggingReplicator()).CheckFlag(EAIDebugDrawDataView::GameView1)) 		{ 			PrintString(DefaultContext, FColor::Green, TEXT("\nMY GAME DATA\n")); 			 DrawCustomData(PC, InDebugComponent); 		} 	#endif 	}`

Copy full snippet
```
GDTHUDComponent.h // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "GameplayDebuggingHUDComponent.h" #include "GDTHUDComponent.generated.h" UCLASS(notplaceable) class AGDTHUDComponent: public AGameplayDebuggingHUDComponent { GENERATED\_UCLASS\_BODY() protected: virtual void DrawGameSpecificView(APlayerController\* PC, class UGameplayDebuggingComponent \*DebugComponent) override; virtual void GetKeyboardDesc(TArray<FDebugCategoryView>& Categories) override; void DrawCustomData(APlayerController\* PC, class UGameplayDebuggingComponent \*DebugComponent); }; GDTHUDComponent.cpp // Copyright Epic Games, Inc. All Rights Reserved. #include "MyGameProject.h" #include "GDTComponent.h" #include "GDTHUDComponent.h" AGDTHUDComponent::AGDTHUDComponent(const class FPostConstructInitializeProperties& PCIP) : Super(PCIP) { } void AGDTHUDComponent::DrawCustomData(APlayerController\* PC, class UGameplayDebuggingComponent \*DebugComponent) { #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) const UGDTComponent\* MyComp = Cast<UGDTComponent>(DebugComponent); if (MyComp) { PrintString(DefaultContext, FString::Printf(TEXT("{white}Test data: {red}%f\\n"), MyComp->TestData)); } #endif } void AGDTHUDComponent::GetKeyboardDesc(TArray<FDebugCategoryView>& Categories) { Super::GetKeyboardDesc(Categories); #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) Categories.Add(FDebugCategoryView(EAIDebugDrawDataView::GameView1, TEXT("MyData"))); #endif } void AGDTHUDComponent::DrawGameSpecificView(APlayerController\* PC, class UGameplayDebuggingComponent \*InDebugComponent) { Super::DrawGameSpecificView(PC, InDebugComponent); #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST) if (InDebugComponent && GameplayDebuggerSettings(GetDebuggingReplicator()).CheckFlag(EAIDebugDrawDataView::GameView1)) { PrintString(DefaultContext, FColor::Green, TEXT("\\nMY GAME DATA\\n")); DrawCustomData(PC, InDebugComponent); } #endif }

Now the new category is ready, and it can be used to debug project specific data.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c7e73d3-f7fa-4429-854d-4be342837ebf/image_4.jpg)

To draw debug information in colors, the `PrintString` function can use tags in strings, to change the active color. This makes it easier to draw strings with different colors.

```
	`void PrintString(FPrintContext& Context, const FString& InString ); 	void PrintString(FPrintContext& Context, const FColor& InColor, const FString& InString ); 	PrintString(DefaultContext, FColor::Green, TEXT("Whole text in green")); 	PrintString(DefaultContext, TEXT("String {green}in green, {red}in red {white}or {R=0,G=0,B=255,A=255}in blue"));`

Copy full snippet
```
void PrintString(FPrintContext& Context, const FString& InString ); void PrintString(FPrintContext& Context, const FColor& InColor, const FString& InString ); PrintString(DefaultContext, FColor::Green, TEXT("Whole text in green")); PrintString(DefaultContext, TEXT("String {green}in green, {red}in red {white}or {R=0,G=0,B=255,A=255}in blue"));

The last `PrintString` function generates a string with 4 different colors.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f7d5d12-6941-4dec-816a-690cc71c0741/image_5.jpg)