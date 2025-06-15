# Replicate Actor Properties

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:04

---

Your Unreal Engine class might have properties you want to replicate in your multiplayer game. Unreal Engine actors maintain a list of all [properties](/documentation/en-us/unreal-engine/unreal-engine-uproperties) with the `Replicated` and `ReplicatedUsing` metadata specifiers. When a property is marked with a `Replicated` or `ReplicatedUsing` metadata specifier during multiplayer gameplay, the server sends an update to each connected client whenever a replicated property changes its value. Each client applies the updated value to its local version of the actor.

This page includes information on:

-   Replicating Actor Properties
-   Adding Replication Conditions
-   Customizing Conditional Replication
-   Replicating Object References

## Replicate Actor Properties

In general, you have two primary options to replicate actor properties:

-   `Replicated`
-   `ReplicatedUsing`

These are both property metadata specifiers used by Unreal Engine's reflection system. `Replicated` properties provide property replication with the option to specify certain conditions that limit replication of properties to certain connections, or custom replication conditions where you can define your own logic for property replication. `ReplicatedUsing` properties require you to provide a RepNotify function that is called on clients whenever the associated property is replicated.

You can also specify a property to *not* replicate with the `NotReplicated` specifier. This specifier might not seem like a useful specifier at first, but it can be helpful to set a property within a replicated struct to not replicate.

### Add a Replicated Property

Suppose you have an `AActor`\-derived class named `ADerivedActor`, and this class has a property `Health` that you need replicated. To replicate an actor property with the `Replicated` specifier, follow these steps:

1.  In your `DerivedActor.h` file, add the `Replicated` metadata specifier to your `Health` property:
    
    DerivedActor.h
    
    ```
         `#pragma once        #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:          // Property to replicate          UPROPERTY(Replicated)          uint32 Health;           // Derived Actor constructor          ADerivedActor(const class FPostConstructInitializeProperties & PCIP);      };`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: // Property to replicate UPROPERTY(Replicated) uint32 Health; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); };
2.  Ensure that the `ADerivedActor` is set to replicate within the derived actor's constructor:
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"       ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; }
3.  Override the `GetLifetimeReplicatedProps` function and add a macro call to replicate the `Health` property for the lifetime of the derived actor instance:
    
    DerivedActor.h
    
    ```
         `#pragma once        #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:          // Property to replicate          UPROPERTY(Replicated)          uint32 Health;           // Derived Actor constructor          ADerivedActor(const class FPostConstructInitializeProperties & PCIP);           // Override Replicate Properties function          virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;      };`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: // Property to replicate UPROPERTY(Replicated) uint32 Health; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); // Override Replicate Properties function virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override; };
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"      #include "Net/UnrealNetwork.h"       ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }       void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const      {          // Call the Super          Super::GetLifetimeReplicatedProps(OutLifetimeProps);           // Add properties to replicated for the derived class          DOREPLIFETIME(ADerivedActor, Health);      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; } void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add properties to replicated for the derived class DOREPLIFETIME(ADerivedActor, Health); }

### Add a Replicated Using Property

You have seen that you can replicate an actor property with the `Replicated` specifier inside a `UPROPERTY` macro. You can perform a specific action each time a variable is replicated with the `ReplicatedUsing` specifier. To perform an action each time your property is replicated, you can use the `ReplicatedUsing` specifier and an associated RepNotify. A **RepNotify** is the `OnRep_` function that is called on the client when a property with the `ReplicatedUsing` specifier is replicated.

Suppose you have an `AActor`\-derived class named `ADerivedActor` and this class has a property `Health` that you need replicated. To specify a property as a `ReplicatedUsing` property, follow these steps:

1.  In your `DerivedActor.h` file, add the `ReplicatedUsing` metadata specifier to your `Health` property. In this metadata, you must specify the name of the function that is called when this property replicates. The format of this RepNotify function name is `OnRep_` followed by whatever you choose to name the function.
    
    DerivedActor.h
    
    ```
         `#pragma once        #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:          // Property to replicate with RepNotify          UPROPERTY(ReplicatedUsing=OnRep_HealthUpdate)          uint32 Health;           // Derived Actor constructor          ADerivedActor(const class FPostConstructInitializeProperties & PCIP);      };`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: // Property to replicate with RepNotify UPROPERTY(ReplicatedUsing=OnRep\_HealthUpdate) uint32 Health; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); };
2.  Ensure that the `ADerivedActor` is set to replicate within the derived actor's constructor:
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"      #include "Net/UnrealNetwork.h"       ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; }
3.  Override the `GetLifetimeReplicatedProps` function and add a macro call to replicate the `Health` property for the lifetime of the derived actor instance:
    
    DerivedActor.h
    
    ```
         `#pragma once        #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:          // Property to replicate with RepNotify          UPROPERTY(ReplicatedUsing=OnRep_HealthUpdate)          uint32 Health;           // Derived Actor constructor          ADerivedActor(const class FPostConstructInitializeProperties & PCIP);           // Override Replicate Properties function          virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;      };`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: // Property to replicate with RepNotify UPROPERTY(ReplicatedUsing=OnRep\_HealthUpdate) uint32 Health; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); // Override Replicate Properties function virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override; };
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"      #include "Net/UnrealNetwork.h"       ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }       void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const      {          // Call the Super          Super::GetLifetimeReplicatedProps(OutLifetimeProps);           // Add properties to replicated for the derived class          DOREPLIFETIME(ADerivedActor, Health);      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; } void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add properties to replicated for the derived class DOREPLIFETIME(ADerivedActor, Health); }
4.  Implement the property's associated RepNotify:
    
    DerivedActor.h
    
    ```
         `#pragma once        #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:          // Property to replicate with RepNotify          UPROPERTY(ReplicatedUsing=OnRep_HealthUpdate)          uint32 Health;           // Derived Actor constructor          ADerivedActor(const class FPostConstructInitializeProperties & PCIP);           // Override Replicate Properties function          virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;           // Health's associated RepNotify          UFUNCTION()          void OnRep_HealthUpdate();      };`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: // Property to replicate with RepNotify UPROPERTY(ReplicatedUsing=OnRep\_HealthUpdate) uint32 Health; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); // Override Replicate Properties function virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override; // Health's associated RepNotify UFUNCTION() void OnRep\_HealthUpdate(); };
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"      #include "Net/UnrealNetwork.h"       ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }       void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const      {          // Call the Super          Super::GetLifetimeReplicatedProps(OutLifetimeProps);           // Add properties to replicated for the derived class          DOREPLIFETIME(ADerivedActor, Health);      }       void ADerivedActor::OnRep_HealthUpdate()      {          UE_LOG(LogTemp, Log, TEXT("OnRep_HealthUpdate"))           // Add custom OnRep logic      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; } void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add properties to replicated for the derived class DOREPLIFETIME(ADerivedActor, Health); } void ADerivedActor::OnRep\_HealthUpdate() { UE\_LOG(LogTemp, Log, TEXT("OnRep\_HealthUpdate")) // Add custom OnRep logic }

#### Usage of Parameters in RepNotify

Unreal Engine's replication system supports passing a parameter in a property's RepNotify that is the same type as the replicated property. If you pass a parameter in a RepNotify, the replication system will automatically pass the previous value of the replicated property into the RepNotify call. To pass the previous replicated property value to the `OnRep_` function for the `Health` example, use the following:

DerivedActor.h

```
	`#pragma once   	#include "DerivedActor.generated.h"  	UCLASS() 	class ADerivedActor : public AActor 	{ 		GENERATED_BODY()  	public:  		// Replicated Property using OnRep_Value 		UPROPERTY(ReplicatedUsing=OnRep_Value) 		int32 HealthValue1;  		// Replicated Property using OnRep_ConstRef 		UPROPERTY(ReplicatedUsing=OnRep_ConstRef) 		int32 HealthValue2;  		// Replicated Property using OnRep_NoParam 		UPROPERTY(ReplicatedUsing=OnRep_NoParam) 		int32 HealthValue3;  		// Signature to pass copy of the last value 		UFUNCTION() 		void OnRep_Value(int32 LastHealthValue);  		// Signature to pass const reference 		UFUNCTION() 		void OnRep_ConstRef(const int32& LastHealthValue);  		// Signature to pass no parameter 		UFUNCTION() 		void OnRep_NoParam();  		// Derived Actor constructor 		ADerivedActor(const class FPostConstructInitializeProperties & PCIP); 	};`
Copy full snippet
```
#pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: // Replicated Property using OnRep\_Value UPROPERTY(ReplicatedUsing=OnRep\_Value) int32 HealthValue1; // Replicated Property using OnRep\_ConstRef UPROPERTY(ReplicatedUsing=OnRep\_ConstRef) int32 HealthValue2; // Replicated Property using OnRep\_NoParam UPROPERTY(ReplicatedUsing=OnRep\_NoParam) int32 HealthValue3; // Signature to pass copy of the last value UFUNCTION() void OnRep\_Value(int32 LastHealthValue); // Signature to pass const reference UFUNCTION() void OnRep\_ConstRef(const int32& LastHealthValue); // Signature to pass no parameter UFUNCTION() void OnRep\_NoParam(); // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); };

DerivedActor.cpp

```
	`#include "DerivedActor.h" 	#include "Net/UnrealNetwork.h"  	ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) 	{ 		bReplicates = true; 	}  	void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const 	{ 		// Call the Super 		Super::GetLifetimeReplicatedProps(OutLifetimeProps);  		// Add properties to replicated for the derived class 		DOREPLIFETIME(ADerivedActor, HealthValue1); 		DOREPLIFETIME(ADerivedActor, HealthValue2); 		DOREPLIFETIME(ADerivedActor, HealthValue3); 	}  	void ADerivedActor::OnRep_Value(int32 LastHealthValue) 	{ 		UE_LOG(LogTemp, Log, TEXT("OnRep_Value with value. Last value: %d"), LastHealthValue) 		// Add custom OnRep logic 	}  	void ADerivedActor::OnRep_ConstRef(const int32& LastHealthValue) 	{ 		UE_LOG(LogTemp, Log, TEXT("OnRep_ConstRef with const ref. Last value: %d"), *LastHealthValue) 		// Add custom OnRep logic 	}  	void ADerivedActor::OnRep_NoParam() 	{ 		UE_LOG(LogTemp, Log, TEXT("OnRep_NoParam with no parameter.")) 		// Add custom OnRep logic 	}`
Copy full snippet
```
#include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; } void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add properties to replicated for the derived class DOREPLIFETIME(ADerivedActor, HealthValue1); DOREPLIFETIME(ADerivedActor, HealthValue2); DOREPLIFETIME(ADerivedActor, HealthValue3); } void ADerivedActor::OnRep\_Value(int32 LastHealthValue) { UE\_LOG(LogTemp, Log, TEXT("OnRep\_Value with value. Last value: %d"), LastHealthValue) // Add custom OnRep logic } void ADerivedActor::OnRep\_ConstRef(const int32& LastHealthValue) { UE\_LOG(LogTemp, Log, TEXT("OnRep\_ConstRef with const ref. Last value: %d"), \*LastHealthValue) // Add custom OnRep logic } void ADerivedActor::OnRep\_NoParam() { UE\_LOG(LogTemp, Log, TEXT("OnRep\_NoParam with no parameter.")) // Add custom OnRep logic }

#### Differences with RepNotify in C++ and Blueprint

RepNotifies work differently in Blueprint than they do in C++. In Blueprint, a `Set` node on a replicated property automatically calls that property's RepNotify function if it has one defined in Blueprint. Generally, Blueprint macros and functions that take properties by reference do not call the RepNotify, even if they modify the value.

### Add a Not Replicated Property

As previously mentioned, the `NotReplicated` specifier is useful for marking a property not to replicate within a replicated struct. The following code snippets provide an example of a not replicated property within a replicated struct.

DerivedActor.h

```
	`#pragma once   	#include "DerivedActor.generated.h"  	USTRUCT() 	struct FMyStruct 	{ 		GENERATED_BODY()  		UPROPERTY() 		int32 ReplicatedProperty;  		// Not Replicated even though encompassing struct is Replicated 		UPROPERTY(NotReplicated) 		int32 NotReplicatedProperty; 	};  	UCLASS() 	class ADerivedActor : public AActor 	{ 		GENERATED_BODY()  	public: 		UPROPERTY(Replicated) 		FMyStruct ReplicatedStruct;  		// Derived Actor constructor 		ADerivedActor(const class FPostConstructInitializeProperties & PCIP); 	};`
Copy full snippet
```
#pragma once #include "DerivedActor.generated.h" USTRUCT() struct FMyStruct { GENERATED\_BODY() UPROPERTY() int32 ReplicatedProperty; // Not Replicated even though encompassing struct is Replicated UPROPERTY(NotReplicated) int32 NotReplicatedProperty; }; UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: UPROPERTY(Replicated) FMyStruct ReplicatedStruct; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); };

DerivedActor.cpp

```
	`#include "DerivedActor.h" 	#include "Net/UnrealNetwork.h"  	ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) 	{ 		bReplicates = true; 	}  	void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const 	{ 		Super::GetLifetimeReplicatedProps(OutLifetimeProps);  		DOREPLIFETIME(ADerivedActor, ReplicatedStruct); 	}`
Copy full snippet
```
#include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; } void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { Super::GetLifetimeReplicatedProps(OutLifetimeProps); DOREPLIFETIME(ADerivedActor, ReplicatedStruct); }

## Conditional Replication

Once you register a property for replication, you can't unregister it. Properties you set for replication are replicated for the lifetime of the object. The replication system embeds as much information as possible so the system can share work across connections for the same set of properties, thereby saving computation time.

To perform finer control over how a property replicates, you can use replication conditions. By default, every replicated property only replicates on the condition that it has changed. Properties that have not changed do not replicate; therefore, they do not use valuable bandwidth.

### Add a Replication Condition

For more control over how a property replicates, you can add a secondary replication condition. To add a replication condition to your replicated property, use the `DOREPLIFETIME_CONDITION` macro:

DerviedActor.cpp

```
	`#include "DerivedActor.h" 	#include "Net/UnrealNetwork.h"  	void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const 	{ 		// Call the Super 		Super::GetLifetimeReplicatedProps(OutLifetimeProps);  		// Add property replication with a condition 		DOREPLIFETIME_CONDITION(ADerivedActor, Health, COND_OwnerOnly); 	}`
Copy full snippet
```
#include "DerivedActor.h" #include "Net/UnrealNetwork.h" void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add property replication with a condition DOREPLIFETIME\_CONDITION(ADerivedActor, Health, COND\_OwnerOnly); }

Notice that this example uses the `DOREPLIFETIME_CONDITION` macro instead of the `DOREPLIFETIME` macro since the replicated property has a condition.

Replication conditions work for properties that are replicated using both the `Replicated` and the `ReplicatedUsing` specifiers.

### Add a RepNotify Condition

RepNotifies add an additional layer of customization over `Replicated` properties. You can use a RepNotify condition to specify whether the associated RepNotify is called every time the property is replicated or only when the property changes. To add a RepNotify condition, use the `DOREPLIFETIME_CONDITION_NOTIFY` macro:

DerivedActor.cpp

```
	`#include "DerivedActor.h" 	#include "Net/UnrealNetwork.h"  	void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const 	{ 		// Call the Super 		Super::GetLifetimeReplicatedProps(OutLifetimeProps);  		// Add property replication with a condition 		/** 	Use this to always execute RepNotify 		*	Associated OnRep called on client every time property replicates 		*/ 		DOREPLIFETIME_CONDITION_NOTIFY(ADerivedActor, Health, REPNOTIFY_Always);  		/** 	Use this to only execute RepNotify when property changes 		*	Associated OnRep called on client only when property changes 		*/ 		DOREPLIFETIME_CONDITION_NOTIFY(ADerivedActor, Health, REPNOTIFY_OnChanged); 	}`
Copy full snippet
```
#include "DerivedActor.h" #include "Net/UnrealNetwork.h" void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add property replication with a condition /\*\* Use this to always execute RepNotify \* Associated OnRep called on client every time property replicates \*/ DOREPLIFETIME\_CONDITION\_NOTIFY(ADerivedActor, Health, REPNOTIFY\_Always); /\*\* Use this to only execute RepNotify when property changes \* Associated OnRep called on client only when property changes \*/ DOREPLIFETIME\_CONDITION\_NOTIFY(ADerivedActor, Health, REPNOTIFY\_OnChanged); }

Notice that this example uses the `DOREPLIFETIME_CONDITION_NOTIFY` macro instead of the `DOREPLIFETIME` macro since the replicated property has a condition.

If you want even more control over how your property replicates, use the appropriate `DOREPLIFETIME_WITH_PARAMS` macro to specify a `FDoRepLifetimeParams` struct. Remember that more control also means more overhead, use the minimum amount of information for the maximum amount of control needed.

### Replication Condition Reference

The table below contains a list of property replication conditions:

| **Condition** | **Description** |
| --- | --- |
| `COND_None` | No condition and replicates anytime it changes. |
| `COND_InitialOnly` | Only attempts to replicate on the initial bunch. |
| `COND_OwnerOnly` | Only replicates to the actor's owner. |
| `COND_SkipOwner` | Replicates to every connection except the actor's owner. |
| `COND_SimulatedOnly` | Replicates to simulated actors. |
| `COND_AutonomousOnly` | Only replicates to autonomous actors. |
| `COND_SimulatedOrPhysics` | Replicates to simulated or `bRepPhysics` actors. |
| `COND_InitialOrOwner` | Replicates on the initial bunch, or to the actor's owner. |
| `COND_Custom` | No particular condition, but has the ability to toggle on or off. See [Custom Property Replication](/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine#custompropertyreplication) for more information. |
| `COND_ReplayOrOwner` | Only replicates to the replay connection, or to the actor's owner. |
| `COND_ReplayOnly` | Only replicates to the replay connection. |
| `COND_SimulatedOnlyNoReplay` | Only replicates to simulated actors, but not to replay connections. |
| `COND_SimulatedOrPhysicsNoReplay` | Replicates to simulated or `bRepPhysics` actors, but not replay connections. |
| `COND_SkipReplay` | Does not replicate to the replay connection. |
| `COND_Dynamic` | Override the condition at runtime. Defaults to always replicate until you override it to a new condition. |
| `COND_Never` | Never replicates. |

### Custom Property Replication

For finer control over when an actor property replicates, you can use the `COND_Custom` replication condition in conjunction with the `DOREPLIFETIME_ACTIVE_OVERRIDE` macro. This macro helps you create any custom condition to dictate when a property replicates. This replication is dictated per actor, not per connection. As a result, it is not safe to use a state that can change per connection in your custom condition.

#### Add a Custom Replication Condition

To override property replication with a custom condition, follow these steps:

1.  Follow the first two steps in the [Add a Replicated Property](/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine#addareplicatedproperty) section.
    
2.  Override the `GetLifetimeReplicatedProps` function and add a macro call to replicate the `Health` property for the lifetime of the derived actor instance with the `COND_Custom` replication condition:
    
    DerivedActor.h
    
    ```
         `#pragma once        #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:          UPROPERTY(Replicated)          int32 Health;           virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;           // Derived Actor constructor          ADerivedActor(const class FPostConstructInitializeProperties & PCIP);      };`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: UPROPERTY(Replicated) int32 Health; virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); };
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"      #include "Net/UnrealNetwork.h"       ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }       void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const      {          // Call the Super          Super::GetLifetimeReplicatedProps(OutLifetimeProps);           // Add properties to replicated for the derived class          DOREPLIFETIME_CONDITION(ADerivedActor, Health, COND_Custom);      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; } void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add properties to replicated for the derived class DOREPLIFETIME\_CONDITION(ADerivedActor, Health, COND\_Custom); }
3.  Define the property or function that provides a boolean expression for your custom replication condition override:
    
    DerivedActor.h
    
    ```
         `#pragma once        #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:           UPROPERTY(Replicated)          int32 Health;           virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override; 			          // Derived Actor constructor          ADerivedActor(const class FPostConstructInitializeProperties & PCIP);           // Custom Replication Condition override function          bool IsInvincible();      };`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: UPROPERTY(Replicated) int32 Health; virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); // Custom Replication Condition override function bool IsInvincible(); };
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"      #include "Net/UnrealNetwork.h"       ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }       void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const      {          // Call the Super          Super::GetLifetimeReplicatedProps(OutLifetimeProps);           // Add properties to replicated for the derived class          DOREPLIFETIME_CONDITION(ADerivedActor, Health, COND_Custom);      }       bool IsInvincible()      {          bool bIsInvincible = false;           // Custom logic to determine invincibility...           return bIsInvincible;      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; } void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add properties to replicated for the derived class DOREPLIFETIME\_CONDITION(ADerivedActor, Health, COND\_Custom); } bool IsInvincible() { bool bIsInvincible = false; // Custom logic to determine invincibility... return bIsInvincible; }
4.  Register your custom replication condition override in your derived class' `PreReplication` function:
    
    DerivedActor.h
    
    ```
         `#pragma once        #include "DerivedActor.generated.h"       UCLASS()      class ADerivedActor : public AActor      {          GENERATED_BODY()       public:          UPROPERTY(Replicated)          int32 Health;           virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;           // Derived Actor constructor          ADerivedActor(const class FPostConstructInitializeProperties & PCIP);           virtual void PreReplication(IRepChangedPropertyTracker& ChangedPropertyTracker) override;           // Custom Replication Condition override function          bool IsInvincible();      };`
    Copy full snippet
    ```
    #pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: UPROPERTY(Replicated) int32 Health; virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); virtual void PreReplication(IRepChangedPropertyTracker& ChangedPropertyTracker) override; // Custom Replication Condition override function bool IsInvincible(); };
    
    DerivedActor.cpp
    
    ```
         `#include "DerivedActor.h"      #include "Net/UnrealNetwork.h"       ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP)      {          bReplicates = true;      }       void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const      {          // Call the Super          Super::GetLifetimeReplicatedProps(OutLifetimeProps);           // Add properties to replicated for the derived class          DOREPLIFETIME_CONDITION(ADerivedActor, Health, COND_Custom);      }       /**	Function where the Custom condition is registered.      */      void ADerivedActor::PreReplication(IRepChangedPropertyTracker& ChangedPropertyTracker)      {          // Call the Super          Super::PreReplication(ChangedPropertyTracker);           /** Use a custom property replication condition          *	In this case, a function IsInvincible()          *	If the actor is invincible, don't replicate Health          */          DOREPLIFETIME_ACTIVE_OVERRIDE(ADerivedActor, Health, !IsInvincible());      }       bool IsInvincible()      {          bool bIsInvincible = false;           // Custom logic to determine invincibility...           return bIsInvincible;      }`
    Copy full snippet
    ```
    #include "DerivedActor.h" #include "Net/UnrealNetwork.h" ADerivedActor::ADerivedActor(const class FPostConstructInitializeProperties & PCIP) : Super(PCIP) { bReplicates = true; } void ADerivedActor::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const { // Call the Super Super::GetLifetimeReplicatedProps(OutLifetimeProps); // Add properties to replicated for the derived class DOREPLIFETIME\_CONDITION(ADerivedActor, Health, COND\_Custom); } /\*\* Function where the Custom condition is registered. \*/ void ADerivedActor::PreReplication(IRepChangedPropertyTracker& ChangedPropertyTracker) { // Call the Super Super::PreReplication(ChangedPropertyTracker); /\*\* Use a custom property replication condition \* In this case, a function IsInvincible() \* If the actor is invincible, don't replicate Health \*/ DOREPLIFETIME\_ACTIVE\_OVERRIDE(ADerivedActor, Health, !IsInvincible()); } bool IsInvincible() { bool bIsInvincible = false; // Custom logic to determine invincibility... return bIsInvincible; }

`Health` now only replicates as long as `IsInvincible` returns false.

A custom replication condition can do anything that the predefined replication conditions can and more, so why not use custom conditions all the time?

-   **Speed:** Custom replication conditions take more resources and more time.
-   **Connection:** Custom replication conditions cannot change on a per-connection basis.

#### Custom Property Replication Macros

There are a few custom property replication macros that have a few differences that you should be aware of. All of these macros use the function `FNetPropertyConditionManager::SetPropertyActiveOverride`. These macros all build an `FRepPropertyDescriptor` struct from the given macro parameters. The difference between the macros is when the descriptor struct is built and whether or not it works for replicated arrays. The following table describes the differences between these macros:

| **Macro** | **Compile Time or Runtime** | **Works with Arrays** |
| --- | --- | --- |
| `DOREPLIFETIME_ACTIVE_OVERRIDE` | Runtime | Yes |
| `DOREPLIFETIME_ACTIVE_OVERRIDE_FAST` | Compile time | No |
| `DOREPLIFETIME_ACTIVE_OVERRIDE_FAST_STATIC_ARRAY` | Compile time | Yes |

The `_FAST` macro versions build the replication property descriptor struct at compile time. This saves CPU cycle time since the replication system does not need to search for the provided `UPROPERTY`, and then build the struct at runtime.

## Replicate Object References

Replication of object references is automatically handled by Unreal Engine's replication system. If you have a `UObject` property that is replicated, references to that object are sent over network connections as a `FNetworkGUID` that is assigned by the authoritative server. The server then notifies all connected clients of this assignment.

#### Add a Replicated Object Reference

To replicate an object reference, mark a `UObject` property as replicated:

DerivedActor.h

```
	`#pragma once   	#include "DerivedActor.generated.h"  	UCLASS() 	class ADerivedActor : public AActor 	{ 		GENERATED_BODY()  	public: 		UPROPERTY(Replicated) 		AActor* Owner;  		// Derived Actor constructor 		ADerivedActor(const class FPostConstructInitializeProperties & PCIP); 	};`
Copy full snippet
```
#pragma once #include "DerivedActor.generated.h" UCLASS() class ADerivedActor : public AActor { GENERATED\_BODY() public: UPROPERTY(Replicated) AActor\* Owner; // Derived Actor constructor ADerivedActor(const class FPostConstructInitializeProperties & PCIP); };

The Owner property is a replicated reference to the actor that this property refers to.

#### Guidelines For Network Object References

For an object to be legally referenced over the network, it must be supported for networking. To check if an object is supported for networking, call `UObject::IsSupportedForNetworking`.

The following objects can have references to them replicated over a network connection:

-   Replicated actors
-   Stably-named, non-replicated actors
-   Replicated components
-   Stably-named, non-replicated actor components
-   Any non-actor, non-component UObject from a loaded package

#### Stably Named Objects

**Stably Named Objects** are objects that exist both on the server and the client, and have the same name on both. Actors are stably named if they were loaded directly from packages, not spawned during gameplay.

Actor components are stably named if:

-   Loaded directly from a package
-   Added with simple construction scripts
-   Manually marked via `UActorComponent::SetNetAddressable`.
    -   Only use this when you know you are manually naming the actor component so it has the same name on the server and client. A good example of this are components added in a `AActor` C++ constructor.

## Property Replication Reference

The following table describes property replication macros available in Unreal Engine, in addition to:

-   The function to call the macro from.
-   Whether the associated `FRepPropertyDescriptor` is constructed at compile time or runtime.
-   Whether the macro works with arrays.

| **Macro** | **Description** | **Where to Call Macro** | **Compile Time or Runtime** | **Works with Arrays** |
| --- | --- | --- | --- | --- |
| `DOREPLIFETIME` | Replicate a property with no conditions or customization. | `GetLifetimeReplicatedProps` | Runtime | Yes |
| `DOREPLIFETIME_WITH_PARAMS` | Replicate a property with an `FDoRepLifetimeParams` struct to control how it is replicated. | `GetLifetimeReplicatedProps` | Runtime | Yes |
| `DOREPLIFETIME_WITH_PARAMS_FAST` | Replicate a property with an `FDoRepLifetimeParams` struct to control how it is replicated. | `GetLifetimeReplicatedProps` | Compile Time | No |
| `DOREPLIFETIME_WITH_PARAMS_FAST_STATIC_ARRAY` | Replicate a property with an `FDoRepLifetimeParams` struct to control how it is replicated. | `GetLifetimeReplicatedProps` | Compile Time | Yes |
| `DOREPLIFETIME_CONDITION` | Replicate a property with an `ELifetimeCondition`. | `GetLifetimeReplicatedProps` | Runtime | Yes |
| `DOREPLIFETIME_CONDITION_NOTIFY` | Replicate a property with a `ELifetimeRepNotifyCondition`. | `GetLifetimeReplicatedProps` | Runtime | Yes |
| `DOREPLIFETIME_ACTIVE_OVERRIDE` | Replicate a property with a custom condition. Must be accompanied by a call to `DOREPLIFETIME_CONDITION(<CLASS>, <PROPERTY>, COND_Custom)`. | `PreReplication` | Runtime | Yes |
| `DOREPLIFETIME_ACTIVE_OVERRIDE_FAST` | Replicate a property with a custom condition. Must be accompanied by a call to `DOREPLIFETIME_CONDITION(<CLASS>, <PROPERTY>, COND_Custom)`. | `PreReplication` | Compile Time | No |
| `DOREPLIFETIME_ACTIVE_OVERRIDE_FAST_STATIC_ARRAY` | Replicate a property with a custom condition. Must be accompanied by a call to `DOREPLIFETIME_CONDITION(<CLASS>, <PROPERTY>, COND_Custom)`. | `PreReplication` | Compile Time | Yes |

You can find the definitions for these macros in `Engine/Source/Runtime/Engine/Public/Net/UnrealNetwork.h`.