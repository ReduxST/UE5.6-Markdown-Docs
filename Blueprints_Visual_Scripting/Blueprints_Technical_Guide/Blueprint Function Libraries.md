# Blueprint Function Libraries

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-function-libraries-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-function-libraries-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:39

---

Often during the development of your project, you may discover the need for a set of functions that make development easier. These functions typically are stateless and reused across a variety of gameplay code. This need may present itself when building with Blueprints. In a previous section of this manual, you saw how to expose your game objects' functions and properties to Blueprints. However, if you want to expose shared utility functions, you don't necessarily want to tie them to a specific gameplay object type. For those cases, we have **Blueprint Function Libraries**.

Blueprint Function Libraries are a collection of static functions that provide utility functionality not tied to a particular gameplay object. These libraries can be grouped into logical function sets, e.g. AI Blueprint Library, or contain utility functions that provide access to many different functional areas, e.g. System Blueprint Library.

Creating a Blueprint Function Library is very similar to exposing functions to Blueprints using the `UFUNCTION()` macro. Instead of deriving from an Actor or directly from `UObject` all Blueprint Libraries inherit from `UBlueprintFunctionLibrary`. They should also contain only static methods. The code below is a snippet from the Analytics Blueprint Library, showing how to setup your library class.

```
	`UCLASS() 	class UAnalyticsBlueprintLibrary : 		public UBlueprintFunctionLibrary 	{ 		GENERATED_UCLASS_BODY() 		/** Starts an analytics session without any custom attributes specified */ 		UFUNCTION(BlueprintCallable, Category="Analytics") 		static bool StartSession();`
Copy full snippet
```
UCLASS() class UAnalyticsBlueprintLibrary : public UBlueprintFunctionLibrary { GENERATED\_UCLASS\_BODY() /\*\* Starts an analytics session without any custom attributes specified \*/ UFUNCTION(BlueprintCallable, Category="Analytics") static bool StartSession();

As you can see in the example above, a Blueprint Function Library is indirectly a `UObject` derived and therefore requires the standard `UCLASS()` and `GENERATED_UCLASS_BODY()` macros. It decorates the functions that are to be callable from Blueprints with the `UFUNCTION()` macro. Functions in a Blueprint Function Library can be designated as BlueprintCallable or BlueprintPure depending on whether the calls have side effects or not.

See `Engine/Plugins/Runtime/Analytics/AnalyticsBlueprintLibrary` for the full source code.

Below is the implementation of the `StartSession()` function:

```
	`bool UAnalyticsBlueprintLibrary::StartSession() 	{ 		TSharedPtr<IAnalyticsProvider> Provider = FAnalytics::Get().GetDefaultConfiguredProvider(); 		if (Provider.IsValid()) 		{ 			return Provider->StartSession(); 		} 		else 		{ 			UE_LOG(LogAnalyticsBPLib, Warning, TEXT("StartSession: Failed to get the default analytics provider. Double check your [Analytics] configuration in your INI")); 		} 		return false; 	}`
Copy full snippet
```
bool UAnalyticsBlueprintLibrary::StartSession() { TSharedPtr<IAnalyticsProvider> Provider = FAnalytics::Get().GetDefaultConfiguredProvider(); if (Provider.IsValid()) { return Provider->StartSession(); } else { UE\_LOG(LogAnalyticsBPLib, Warning, TEXT("StartSession: Failed to get the default analytics provider. Double check your \[Analytics\] configuration in your INI")); } return false; }

The implementation above interacts with a non-UObject derived singleton object. This is a good way to expose 3rd party library functions to Blueprints or to interact with C++ classes that don't have `UObject` support. The code below is an example of a Blueprint Function Library method that performs some common work to find the AIController for a controlled actor:

```
	`AAIController* UAIBlueprintHelperLibrary::GetAIController(AActor* ControlledActor) 	{ 		APawn* AsPawn = Cast<APawn>(ControlledActor); 		if (AsPawn != nullptr) 		{ 			return Cast<AAIController>(AsPawn->GetController()); 		} 		return Cast<AAIController>(ControlledActor); 	}`
Copy full snippet
```
AAIController\* UAIBlueprintHelperLibrary::GetAIController(AActor\* ControlledActor) { APawn\* AsPawn = Cast<APawn>(ControlledActor); if (AsPawn != nullptr) { return Cast<AAIController>(AsPawn->GetController()); } return Cast<AAIController>(ControlledActor); }

This function takes what would be multiple Blueprint nodes and rolls that into a single node. Of course, you could have made a function in Blueprints for this, but if it's called often the C++ version will yield better performance.