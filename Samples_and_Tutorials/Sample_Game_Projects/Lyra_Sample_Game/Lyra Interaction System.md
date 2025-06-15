# Lyra Interaction System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lyra-sample-game-interaction-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lyra-sample-game-interaction-system-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:36

---

## Lyra Interaction System

Lyra uses its interaction [Interface](/documentation/en-us/unreal-engine/interfaces-in-unreal-engine)/[IInterface](/documentation/en-us/unreal-engine/API/Runtime/CoreUObject/UObject/IInterface) through its own [Gameplay Ability](/documentation/en-us/unreal-engine/gameplay-ability-system-for-unreal-engine)/[UGameplayAbility](/documentation/en-us/unreal-engine/API/Plugins/GameplayAbilities/Abilities/UGameplayAbility) (ULyraGameplayAbility\_Interact) which establishes a cause and effect relationship between how the player Interacts with objects in Lyra, and how those objects interact with the player.

Using the `LyraGameplayAbility_Interact` class, you can manage the logic of how your interactions are called.

**ULyraGameplayAbility\_Interact.h**

```
		`#pragma once 		#include "CoreMinimal.h" 		#include "AbilitySystem/Abilities/LyraGameplayAbility.h" 		#include "Interaction/InteractionQuery.h" 		#include "Interaction/IInteractableTarget.h" 		#include "LyraGameplayAbility_Interact.generated.h"  		class FIndicatorDescriptor; 		/**  		 * ULyraGameplayAbility_Interact 		 * 		 * Gameplay ability used for character interacting 		 */ 		UCLASS(Abstract) 		class ULyraGameplayAbility_Interact : public ULyraGameplayAbility 		{ 			GENERATED_BODY() 		public:  			ULyraGameplayAbility_Interact(const FObjectInitializer& ObjectInitializer = FObjectInitializer::Get()); 			virtual void ActivateAbility(const FGameplayAbilitySpecHandle Handle, const FGameplayAbilityActorInfo* ActorInfo, const FGameplayAbilityActivationInfo ActivationInfo, const FGameplayEventData* TriggerEventData) override;  			UFUNCTION(BlueprintCallable) 			void UpdateInteractions(const TArray<FInteractionOption>& InteractiveOptions);  			UFUNCTION(BlueprintCallable) 			void TriggerInteraction();  		protected:  			UPROPERTY(BlueprintReadWrite) 			TArray<FInteractionOption> CurrentOptions;  			TArray<TSharedRef<FIndicatorDescriptor>> Indicators;  		protected:  			UPROPERTY(EditDefaultsOnly) 			float InteractionScanRate = 0.1f;  			UPROPERTY(EditDefaultsOnly) 			float InteractionScanRange = 500;  			UPROPERTY(EditDefaultsOnly) 			TSoftClassPtr<UUserWidget> DefaultInteractionWidgetClass;  		};`

Copy full snippet
```
#pragma once #include "CoreMinimal.h" #include "AbilitySystem/Abilities/LyraGameplayAbility.h" #include "Interaction/InteractionQuery.h" #include "Interaction/IInteractableTarget.h" #include "LyraGameplayAbility\_Interact.generated.h" class FIndicatorDescriptor; /\*\* \* ULyraGameplayAbility\_Interact \* \* Gameplay ability used for character interacting \*/ UCLASS(Abstract) class ULyraGameplayAbility\_Interact : public ULyraGameplayAbility { GENERATED\_BODY() public: ULyraGameplayAbility\_Interact(const FObjectInitializer& ObjectInitializer = FObjectInitializer::Get()); virtual void ActivateAbility(const FGameplayAbilitySpecHandle Handle, const FGameplayAbilityActorInfo\* ActorInfo, const FGameplayAbilityActivationInfo ActivationInfo, const FGameplayEventData\* TriggerEventData) override; UFUNCTION(BlueprintCallable) void UpdateInteractions(const TArray<FInteractionOption>& InteractiveOptions); UFUNCTION(BlueprintCallable) void TriggerInteraction(); protected: UPROPERTY(BlueprintReadWrite) TArray<FInteractionOption> CurrentOptions; TArray<TSharedRef<FIndicatorDescriptor>> Indicators; protected: UPROPERTY(EditDefaultsOnly) float InteractionScanRate = 0.1f; UPROPERTY(EditDefaultsOnly) float InteractionScanRange = 500; UPROPERTY(EditDefaultsOnly) TSoftClassPtr<UUserWidget> DefaultInteractionWidgetClass; };

`AbilityTask_WaitForInteractableTargets_SingleLineTrace` is a Gameplay [Ability Task](/documentation/en-us/unreal-engine/gameplay-ability-tasks-in-unreal-engine), which performs a line trace and waits in a looped timer until it hits an Actor that implements the interface.

As an example:

A player controlling a LyraPawnActor is low on health, the player directs the Pawn towards a collectible health item pickup. Upon aligning the player's crosshair with the Collectible, and pressing the "Use/Interact" key, a Line Trace is fired from the Pawn. When the trace hits the Collectible, the interaction interface implemented on the Collectible will handle the logic to restore the Player's health to its full amount.

## Interaction Ability Tasks

`UAbilityTask_WaitForInteractableTargets` is used to make a new method of tracing for interactable targets.

As an example:

A player controlling a LyraPawnActor approaches a door that they want to open. Upon aligning the player's crosshair with the door and pressing the "Use" key, a radial menu appears with the options to "Unlock/Lock" the door, or attempt to open the door.

For additional information on Line Traces in Unreal, See [Tracing](/documentation/en-us/unreal-engine/traces-tutorials-in-unreal-engine)

**UAbilityTask\_WaitForInteractableTargets.h**

```
		`#pragma once 		#include "CoreMinimal.h" 		#include "UObject/ObjectMacros.h" 		#include "Abilities/Tasks/AbilityTask.h" 		#include "Engine/EngineTypes.h" 		#include "CollisionQueryParams.h" 		#include "WorldCollision.h" 		#include "Engine/CollisionProfile.h" 		#include "Abilities/GameplayAbilityTargetDataFilter.h" 		#include "Interaction/InteractionOption.h" 		#include "Interaction/InteractionQuery.h" 		#include "Interaction/IInteractableTarget.h" 		#include "AbilityTask_WaitForInteractableTargets.generated.h"  		class AActor; 		class UPrimitiveComponent; 		class UGameplayAbility;  		DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FInteractableObjectsChangedEvent, const TArray<FInteractionOption>&, InteractableOptions);  		UCLASS(Abstract) 		class UAbilityTask_WaitForInteractableTargets : public UAbilityTask 		{ 			GENERATED_UCLASS_BODY()  		public:  			UPROPERTY(BlueprintAssignable) 			FInteractableObjectsChangedEvent InteractableObjectsChanged;  		protected:  			static void LineTrace(FHitResult& OutHitResult, const UWorld* World, const FVector& Start, const FVector& End, FName ProfileName, const FCollisionQueryParams Params); 			void AimWithPlayerController(const AActor* InSourceActor, FCollisionQueryParams Params, const FVector& TraceStart, float MaxRange, FVector& OutTraceEnd, bool bIgnorePitch = false) const; 			static bool ClipCameraRayToAbilityRange(FVector CameraLocation, FVector CameraDirection, FVector AbilityCenter, float AbilityRange, FVector& ClippedPosition); 			void UpdateInteractableOptions(const FInteractionQuery& InteractQuery, const TArray<TScriptInterface<IInteractableTarget>>& InteractableTargets); 			FCollisionProfileName TraceProfile;  			// Does the trace affect the aiming pitch 			bool bTraceAffectsAimPitch = true;  			TArray<FInteractionOption> CurrentOptions;  		};`

Copy full snippet
```
#pragma once #include "CoreMinimal.h" #include "UObject/ObjectMacros.h" #include "Abilities/Tasks/AbilityTask.h" #include "Engine/EngineTypes.h" #include "CollisionQueryParams.h" #include "WorldCollision.h" #include "Engine/CollisionProfile.h" #include "Abilities/GameplayAbilityTargetDataFilter.h" #include "Interaction/InteractionOption.h" #include "Interaction/InteractionQuery.h" #include "Interaction/IInteractableTarget.h" #include "AbilityTask\_WaitForInteractableTargets.generated.h" class AActor; class UPrimitiveComponent; class UGameplayAbility; DECLARE\_DYNAMIC\_MULTICAST\_DELEGATE\_OneParam(FInteractableObjectsChangedEvent, const TArray<FInteractionOption>&, InteractableOptions); UCLASS(Abstract) class UAbilityTask\_WaitForInteractableTargets : public UAbilityTask { GENERATED\_UCLASS\_BODY() public: UPROPERTY(BlueprintAssignable) FInteractableObjectsChangedEvent InteractableObjectsChanged; protected: static void LineTrace(FHitResult& OutHitResult, const UWorld\* World, const FVector& Start, const FVector& End, FName ProfileName, const FCollisionQueryParams Params); void AimWithPlayerController(const AActor\* InSourceActor, FCollisionQueryParams Params, const FVector& TraceStart, float MaxRange, FVector& OutTraceEnd, bool bIgnorePitch = false) const; static bool ClipCameraRayToAbilityRange(FVector CameraLocation, FVector CameraDirection, FVector AbilityCenter, float AbilityRange, FVector& ClippedPosition); void UpdateInteractableOptions(const FInteractionQuery& InteractQuery, const TArray<TScriptInterface<IInteractableTarget>>& InteractableTargets); FCollisionProfileName TraceProfile; // Does the trace affect the aiming pitch bool bTraceAffectsAimPitch = true; TArray<FInteractionOption> CurrentOptions; };

Your chosen AbilityTask for tracing delivers a set of Interactable targets from the `FInteractionQuery` struct.

**struct FInteractionQuery**

```
		`#pragma once 		#include "CoreMinimal.h" 		#include "Abilities/GameplayAbility.h" 		#include "InteractionQuery.generated.h"  		/**  */ 		USTRUCT(BlueprintType) 		struct FInteractionQuery 		{  			GENERATED_BODY()  		public: 			/** The requesting pawn. */ 			UPROPERTY(BlueprintReadWrite) 			TWeakObjectPtr<AActor> RequestingAvatar;  			/** Provides us the capability to specify a controller - this does not need to match the owner of the requesting avatar. */ 			UPROPERTY(BlueprintReadWrite) 			TWeakObjectPtr<AController> RequestingController;  			/** A generic UObject to provide extra data required for the interaction */ 			UPROPERTY(BlueprintReadWrite) 			TWeakObjectPtr<UObject> OptionalObjectData; 		};`

Copy full snippet
```
#pragma once #include "CoreMinimal.h" #include "Abilities/GameplayAbility.h" #include "InteractionQuery.generated.h" /\*\* \*/ USTRUCT(BlueprintType) struct FInteractionQuery { GENERATED\_BODY() public: /\*\* The requesting pawn. \*/ UPROPERTY(BlueprintReadWrite) TWeakObjectPtr<AActor> RequestingAvatar; /\*\* Provides us the capability to specify a controller - this does not need to match the owner of the requesting avatar. \*/ UPROPERTY(BlueprintReadWrite) TWeakObjectPtr<AController> RequestingController; /\*\* A generic UObject to provide extra data required for the interaction \*/ UPROPERTY(BlueprintReadWrite) TWeakObjectPtr<UObject> OptionalObjectData; };

to the method `UAbilityTask_WaitForInteractableTargets::UpdateInteractableOptions`:

```
		`void UAbilityTask_WaitForInteractableTargets::UpdateInteractableOptions(const FInteractionQuery& InteractQuery, const TArray<TScriptInterface<IInteractableTarget>>& InteractableTargets) 		{  			TArray<FInteractionOption> NewOptions;  			for (const TScriptInterface<IInteractableTarget>& InteractiveTarget : InteractableTargets)  			{  				TArray<FInteractionOption> TempOptions;  				FInteractionOptionBuilder InteractionBuilder(InteractiveTarget, TempOptions);  				InteractiveTarget->GatherInteractionOptions(InteractQuery, InteractionBuilder);  				for (FInteractionOption& Option : TempOptions)  				{  					FGameplayAbilitySpec* InteractionAbilitySpec = nullptr;  					// if there is a handle and a target ability system, we're triggering the ability on the target.  					if (Option.TargetAbilitySystem && Option.TargetInteractionAbilityHandle.IsValid())  					{  						// Find the spec  						InteractionAbilitySpec = Option.TargetAbilitySystem->FindAbilitySpecFromHandle(Option.TargetInteractionAbilityHandle);  					}  					// If there's an interaction ability then we're activating it on ourselves.  					else if (Option.InteractionAbilityToGrant)  					{  						// Find the spec  						InteractionAbilitySpec = AbilitySystemComponent->FindAbilitySpecFromClass(Option.InteractionAbilityToGrant);  						if (InteractionAbilitySpec)  						{  							// update the option  							Option.TargetAbilitySystem = AbilitySystemComponent;  							Option.TargetInteractionAbilityHandle = InteractionAbilitySpec->Handle;  						}  					}  					if (InteractionAbilitySpec)  					{  						// Filter any options that we can't activate right now for whatever reason.  						if (InteractionAbilitySpec->Ability->CanActivateAbility(InteractionAbilitySpec->Handle, AbilitySystemComponent->AbilityActorInfo.Get()))  						{  							NewOptions.Add(Option);  						}  					}  				}  			}  			bool bOptionsChanged = false;  			if (NewOptions.Num() == CurrentOptions.Num())  			{  				NewOptions.Sort();  				for (int OptionIndex = 0; OptionIndex < NewOptions.Num(); OptionIndex++)  				{  					const FInteractionOption& NewOption = NewOptions[OptionIndex];  					const FInteractionOption& CurrentOption = CurrentOptions[OptionIndex];  					if (NewOption != CurrentOption)  					{  						bOptionsChanged = true;  						break;  					}  				}  			}  			else  			{  				bOptionsChanged = true;  			}  			if (bOptionsChanged)  			{  				CurrentOptions = NewOptions;  				InteractableObjectsChanged.Broadcast(CurrentOptions);  			}  		}`
Copy full snippet
```
void UAbilityTask\_WaitForInteractableTargets::UpdateInteractableOptions(const FInteractionQuery& InteractQuery, const TArray<TScriptInterface<IInteractableTarget>>& InteractableTargets) { TArray<FInteractionOption> NewOptions; for (const TScriptInterface<IInteractableTarget>& InteractiveTarget : InteractableTargets) { TArray<FInteractionOption> TempOptions; FInteractionOptionBuilder InteractionBuilder(InteractiveTarget, TempOptions); InteractiveTarget->GatherInteractionOptions(InteractQuery, InteractionBuilder); for (FInteractionOption& Option : TempOptions) { FGameplayAbilitySpec\* InteractionAbilitySpec = nullptr; // if there is a handle and a target ability system, we're triggering the ability on the target. if (Option.TargetAbilitySystem && Option.TargetInteractionAbilityHandle.IsValid()) { // Find the spec InteractionAbilitySpec = Option.TargetAbilitySystem->FindAbilitySpecFromHandle(Option.TargetInteractionAbilityHandle); } // If there's an interaction ability then we're activating it on ourselves. else if (Option.InteractionAbilityToGrant) { // Find the spec InteractionAbilitySpec = AbilitySystemComponent->FindAbilitySpecFromClass(Option.InteractionAbilityToGrant); if (InteractionAbilitySpec) { // update the option Option.TargetAbilitySystem = AbilitySystemComponent; Option.TargetInteractionAbilityHandle = InteractionAbilitySpec->Handle; } } if (InteractionAbilitySpec) { // Filter any options that we can't activate right now for whatever reason. if (InteractionAbilitySpec->Ability->CanActivateAbility(InteractionAbilitySpec->Handle, AbilitySystemComponent->AbilityActorInfo.Get())) { NewOptions.Add(Option); } } } } bool bOptionsChanged = false; if (NewOptions.Num() == CurrentOptions.Num()) { NewOptions.Sort(); for (int OptionIndex = 0; OptionIndex < NewOptions.Num(); OptionIndex++) { const FInteractionOption& NewOption = NewOptions\[OptionIndex\]; const FInteractionOption& CurrentOption = CurrentOptions\[OptionIndex\]; if (NewOption != CurrentOption) { bOptionsChanged = true; break; } } } else { bOptionsChanged = true; } if (bOptionsChanged) { CurrentOptions = NewOptions; InteractableObjectsChanged.Broadcast(CurrentOptions); } }

which will call `IInteractableTarget::GatherInteractionOptions` on each interactable target.

```
		`virtual void GatherInteractionOptions(const FInteractionQuery& InteractQuery, FInteractionOptionBuilder& OptionBuilder) = 0;`

Copy full snippet
```
virtual void GatherInteractionOptions(const FInteractionQuery& InteractQuery, FInteractionOptionBuilder& OptionBuilder) = 0;

Once you update the set of interactable objects, the interaction ability (GA\_Interact) calls the `TriggerInteraction` function when the player focuses on an object to interact with and receives input from the player that they want to interact with that particular object.

Once you invoke the current Option, there are two methods by which interactions can occur. The first method grants an ability to the player's Ability System Component through the function `FInteractionOption::InteractionAbilityToGrant`, using this function is recommended for simple logic such as the Weapon Pickup Actor.

Alternatively, if you're interacting with an object that contains its own Ability System Component to handle complex logic, then you can invoke the `FInteractionOption::TargetAbilitySystem` and the `FInteractionOption::TargetInteractionHandle` functions, this invokes the ability on the interactable object, instead of invoking the ability on the Lyra Character's (Avatar) Ability System Component.

The interaction function `FInteractionOption::InteractionAbilityToGrant` is inherited from the base class of your `ULyraGameplayAbility_Interact` interaction ability, which runs the task function `AbilityTask_GrantNearbyInteraction`, as a ranged loop and timer that collects nearby abilities and grants them to your character before you attempt to interact with them. You can increase the `InteractionScanRate` float to be at a larger radius than your `InteractionRange`, otherwise, replication will not deliver the ability to the client soon enough.

The ability is invoked through the event [Gameplay Tag](/documentation/en-us/unreal-engine/using-gameplay-tags-in-unreal-engine), `FInteractionOption::InteractionEventTag`. This tag needs to match up to a trigger in your ability. For example, the `GA_Collect_Interaction` is triggered when the `Ability.Type.Interact.Collect` event is sent, which is set in the interaction option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b38ddbd0-ab09-4516-b8b7-f8785832579c/interactinterface.png)

`GA_Collect_Interaction` represents only one kind of interaction, it is an ability that provides you the capability to pick up objects on the ground and add them to your inventory. There is no limit to your imagination, you can make an ability to eat Apples on the ground that will refill your player's health, or you could make an ability to open doors, get into a vehicle, or open a chest.

This decoupling behavior provides you with all kinds of different interactions from the central passive interaction scanner.

#### Important Lyra Interaction Terminology

**InteractableTarget** - An Actor or Component that implements the IInteractableTarget interface, this determines what objects in the world can be interacted with.

**InteractionOption** - The "Affordance" or "Option", for example, an apple might provide both a "Collect" and a "Consume".

**InteractionInstigator** - The Pawn (LyraPawnActor) that initiates the interaction. They may or may not implement the `IInteractionInstigator` interface, which allows further customization of options and how they are presented.