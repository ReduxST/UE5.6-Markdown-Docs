# Creating Timelines

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-timelines-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-timelines-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:49

---

Programming Language

×C++

Select an option from the dropdown to see content relevant to it.

## Creating Timelines

You can create and instantiate your own **Timeline Component** in an **Actor** class by following the steps below.

1.  Navigate to your **C++ Classes folder** and click the **Add+**. From the drop down menu select **New C++ Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2510967e-2b64-4745-b4ce-329fdc714423?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2510967e-2b64-4745-b4ce-329fdc714423?resizing_type=fit)
    
2.  Select **Actor** class as a **Parent Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/82200c30-59fc-4ab8-86b0-f8eb9d05b056?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/82200c30-59fc-4ab8-86b0-f8eb9d05b056?resizing_type=fit)
    
    Click image for full size.
    
3.  Name created Actor class **Timeline Actor**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/a4753060-0e69-44a5-adfd-1ba3dc55bb9c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a4753060-0e69-44a5-adfd-1ba3dc55bb9c?resizing_type=fit)
    
    Click image for full size.
    
4.  Navigate to your `TimelineActor.h` file and include following `TimelineComponent` class library.
    
    TimelineActor.h
    
    C++
    
    `#include "Components/TimelineComponent.h"`
    
    #include &quot;Components/TimelineComponent.h&quot;
    
    Copy full snippet(1 line long)
    
5.  Implement the following class declaration inside the TimelineActor class defintion:
    
    TimelineActor.h
    
    C++
    
    `protected:          UPROPERTY(EditAnywhere, BlueprintReadWrite)         UTimelineComponent* ExampleTimelineComp;`
    
    protected: UPROPERTY(EditAnywhere, BlueprintReadWrite) UTimelineComponent\* ExampleTimelineComp;
    
    Copy full snippet(4 lines long)
    
    In this code sample, you use the [Property Specifier Tags](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-uproperties), **EditAnywhere**, and **BlueprintReadWrite**.
    
6.  Navigate to the `TimelineActor.cpp` file, then add the following code to your TimelineActor constructor `ATimelineActor::ATimelineActor()`
    
    TimelineActor.cpp
    
    C++
    
    `ATimelineActor::ATimelineActor()      {          // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.          PrimaryActorTick.bCanEverTick = true;          ExampleTimelineComp = CreateDefaultSubobject<UTimelineComponent>(TEXT("TimelineComponent"));      }`
    
    ATimelineActor::ATimelineActor() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don&#39;t need it. PrimaryActorTick.bCanEverTick = true; ExampleTimelineComp = CreateDefaultSubobject&lt;UTimelineComponent&gt;(TEXT(&quot;TimelineComponent&quot;)); }
    
    Copy full snippet(6 lines long)
    
7.  **Compile** your code.
    
8.  Navigate to the **C++ classes folder**, right-click on your **TimelineActor** and create a Blueprint based on your TimelineActor class. Name it **Bp\_TimelineActor**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/a169b69a-e154-4920-b71d-f124b0048acb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a169b69a-e154-4920-b71d-f124b0048acb?resizing_type=fit)
    
9.  Once you have created your TimelineActor Blueprint, you can view the **Class Defaults**. From the **Components** tab, you should see your example Timeline Component.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2a15cd95-3df9-4d65-845c-8b101a5b416e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2a15cd95-3df9-4d65-845c-8b101a5b416e?resizing_type=fit)
    

### Work-In-Progress Code

TimelineActor.h

C++

```code
`#pragma once 	#include "Components/TimelineComponent.h" 	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "TimelineActor.generated.h"  	UCLASS() 	class CPPTIMELINE_API ATimelineActor : public AActor 	{ 		GENERATED_BODY()`

```

Expand codeCopy full snippet(27 lines long)

TimelineActor.cpp

C++

```code
`#include "TimelineActor.h"  	// Sets default values 	ATimelineActor::ATimelineActor() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true; 		ExampleTimelineComp = CreateDefaultSubobject<UTimelineComponent>(TEXT("TimelineComponent")); 	}`


```

Expand codeCopy full snippet(21 lines long)

## Timeline Variables

When you create a Timeline Component in C++ using `UProperty Specifiers`, it will become available as a variable in your **Components** tab. This may be useful for designers who would like to continue to make iterations to your TimelineComponent via Blueprint Scripting.

[![](https://dev.epicgames.com/community/api/documentation/image/443b21a7-8228-4b93-b192-be5ba5d447a2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/443b21a7-8228-4b93-b192-be5ba5d447a2?resizing_type=fit)

Image above shows using the native C++ Timeline Variable to get the Current Play Rate value of the Timeline in Blueprint.

For a complete list of the available Blueprint Timeline nodes and their functionality please see the [Timeline nodes](https://dev.epicgames.com/documentation/en-us/unreal-engine/timelines-nodes-in-unreal-engine) page.

## Creating a FTimeLineEvent

Timeline Events (`FOnTimelineEvent`) are [Dynamic Delegates](https://dev.epicgames.com/documentation/en-us/unreal-engine/dynamic-delegates-in-unreal-engine) that provide functionality to a Timeline Component to handle an Event. Follow the steps below to create your own `FTimeLineEvent` to be bound to your Timeline Component's finished functionality.

1.  Navigate to `TimelineActor.h` file and declare the following code in the **Class Definition**:
    
    TimelineActor.h
    
    C++
    
    `protected:           //Delegate signature for the function which will handle our Finished event.          FOnTimelineEvent TimelineFinishedEvent;           UFUNCTION()          void TimelineFinishedFunction();`
    
    protected: //Delegate signature for the function which will handle our Finished event. FOnTimelineEvent TimelineFinishedEvent; UFUNCTION() void TimelineFinishedFunction();
    
    Copy full snippet(7 lines long)
    
2.  Navigate to `TimelineActor.cpp` and implement the following code:
    
    TimelineActor.cpp
    
    C++
    
    `void ATimelineActor::TimelineFinishedFunction()       {          UE_LOG(LogTemp, Warning, TEXT("Finished Event Called."));       }`
    
    void ATimelineActor::TimelineFinishedFunction() { UE\_LOG(LogTemp, Warning, TEXT(&quot;Finished Event Called.&quot;)); }
    
    Copy full snippet(4 lines long)
    
3.  Navigate to `ATimelineActor::BeginPlay()` method, and implement the following code:
    
    TimelineActor.cpp
    
    C++
    
    `// Called when the game starts or when spawned       void ATimelineActor::BeginPlay()      {          Super::BeginPlay();           TimelineFinishedEvent.BindUFunction(this, FName("TimelineFinishedFunction"));          ExampleTimelineComp->SetTimelineFinishedFunc(TimelineFinishedEvent);          ExampleTimelineComp->PlayFromStart();      }`
    
    // Called when the game starts or when spawned void ATimelineActor::BeginPlay() { Super::BeginPlay(); TimelineFinishedEvent.BindUFunction(this, FName(&quot;TimelineFinishedFunction&quot;)); ExampleTimelineComp-&gt;SetTimelineFinishedFunc(TimelineFinishedEvent); ExampleTimelineComp-&gt;PlayFromStart(); }
    
    Copy full snippet(10 lines long)
    
    You have now successfully bound your `TimelineFinished` Event to your custom `TimelineFinished` function.
    
4.  Compile your code. Open **Editor** and navigate to the **Content Browser**. Find your **BP\_TimelineActor** and drag off it into the **Level**.
    
    [![image alt text](https://dev.epicgames.com/community/api/documentation/image/28357d14-c481-408c-b8a8-0ca300d76a4f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/28357d14-c481-408c-b8a8-0ca300d76a4f?resizing_type=fit)
    
5.  Press **Play** button. You should see the following message in the **Output Log** window:
    
    [![image alt text](https://dev.epicgames.com/community/api/documentation/image/26badab2-7e7c-4fb6-94f0-f372f00d15af?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/26badab2-7e7c-4fb6-94f0-f372f00d15af?resizing_type=fit)
    

### Finished Code

TimelineActor.h

C++

```code
`#pragma once 	#include "Components/TimelineComponent.h" 	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "TimelineActor.generated.h"  	UCLASS() 	class CPPTIMELINE_API ATimelineActor : public AActor 	{ 		GENERATED_BODY()`

```

Expand codeCopy full snippet(35 lines long)

TimelineActor.cpp

C++

```code
`#include "TimelineActor.h"  	// Sets default values 	ATimelineActor::ATimelineActor() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true; 		ExampleTimelineComp = CreateDefaultSubobject<UTimelineComponent>(TEXT("TimelineComponent")); 	}`


```

Expand codeCopy full snippet(31 lines long)