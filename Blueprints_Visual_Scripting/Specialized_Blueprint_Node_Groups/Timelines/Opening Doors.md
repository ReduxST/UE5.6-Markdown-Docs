# Opening Doors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/opening-doors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/opening-doors-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:14

---

Programming Language

×C++

Select an option from the dropdown to see content relevant to it.

An example C++ **[Timeline](programming-and-scripting/blueprints-visual-scripting/UserGuide/Timelines)** is used to set up a classic proximity-based opening door.

## Creating the Door Actor

1.  Create the new **C++** project based on **Blank** template with **Starter Content** enabled, name it **TimelineDoorActor**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/16553dca-376a-4900-8d76-29f0a03467f3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/16553dca-376a-4900-8d76-29f0a03467f3?resizing_type=fit)
    
    Click image for full size.
    
2.  Navigate to the **Content Browser**, click **C++ Classes** folder, then click **Add (+)** button and select **New C++ Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/d7793964-1e11-4c85-a05b-8d8c67d79be7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d7793964-1e11-4c85-a05b-8d8c67d79be7?resizing_type=fit)
    
    Click image for full size.
    
3.  Select **Actor** as a **Parent Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/85a7bf5a-6284-4c13-8ae3-f3425b84c06c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/85a7bf5a-6284-4c13-8ae3-f3425b84c06c?resizing_type=fit)
    
    Click image for full size.
    
4.  Name created Actor as **DoorActor**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/5f5c800d-9571-4fe2-a9d4-7f7d41f6c007?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5f5c800d-9571-4fe2-a9d4-7f7d41f6c007?resizing_type=fit)
    
    Click image for full size.
    
5.  When new Actor is created, **Visual Studio** automatically opens `DoorActor.h` and `DoorActor.cpp` files. Navigate to the `DoorActor.h` file and declare the following:
    
    DoorActor.h
    
    C++
    
    `#include "Components/TimelineComponent.h"`
    
    #include &quot;Components/TimelineComponent.h&quot;
    
    Copy full snippet(1 line long)
    
6.  Next, in the `DoorActor` class definition, add the following code:
    
    DoorActor.h
    
    C++
    
    ```code
    `protected:           //MeshComponents to represent Door assets          UPROPERTY(VisibleAnywhere, BlueprintReadWrite)          UStaticMeshComponent* DoorFrame;          UPROPERTY(VisibleAnywhere, BlueprintReadWrite)          UStaticMeshComponent* Door;           //TimelineComponent to animate Door meshes          UPROPERTY(VisibleAnywhere, BlueprintReadWrite)`
    
    ```
    
    Expand codeCopy full snippet(15 lines long)
    
7.  Navigate to the `DoorActor.cpp`. You will need to include the following class library to utilize your Box Component.
    
    DoorActor.cpp
    
    C++
    
    `#include "Components/BoxComponent.h"`
    
    #include &quot;Components/BoxComponent.h&quot;
    
    Copy full snippet(1 line long)
    
8.  In the constructor of your `ADoorActor::ADoorActor` declare the following:
    
    DoorActor.cpp
    
    C++
    
    ```code
    `// Sets default values      ADoorActor::ADoorActor()      {          // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.          PrimaryActorTick.bCanEverTick = true;           //Create our Default Components          DoorFrame = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("DoorFrameMesh"));          Door = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("DoorMesh"));          DoorTimelineComp = CreateDefaultSubobject<UTimelineComponent>(TEXT("DoorTimelineComp"));`
    
    ```
    
    Expand codeCopy full snippet(17 lines long)
    
    *Note*: We keep the door's relative transform as an attachment rule, in order to manipulate it later with a custom method for our Door Actor. For further documentation, see [FAttachmentTransformRules](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Engine/FAttachmentTransformRules?application_version=5.5).
    
9.  Compile your code.
    

## Setting Up the Door Static Mesh

You will need to set up the **Static Mesh** assets that will visually represent your DoorFrame and Door Static Mesh components.

1.  From the **Content Browser**, navigate to your **C++ Classes folder**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/ce5d2e5d-69fb-4a06-a534-e0ad67b04565?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ce5d2e5d-69fb-4a06-a534-e0ad67b04565?resizing_type=fit)
    
2.  Right click your **DoorActor** class, select **Create Blueprint Class based on DoorActor**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/ebb5fc07-6cbb-4b32-82a6-885e692c638d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ebb5fc07-6cbb-4b32-82a6-885e692c638d?resizing_type=fit)
    
3.  Name your Blueprint Actor **Bp\_DoorActor** and place it in appropriate folder.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/7829189c-2502-479a-8d6e-0ce0a267d5c2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7829189c-2502-479a-8d6e-0ce0a267d5c2?resizing_type=fit)
    
    Click image for full size.
    
4.  From the **Components** tab, select the **DoorFrame** Static Mesh component.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/9d690f91-0da4-44f3-98a8-ea53e647f363?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9d690f91-0da4-44f3-98a8-ea53e647f363?resizing_type=fit)
    
5.  Navigate to the **Details panel** and change the **Static Mesh** to **SM\_DoorFrame**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/989ed7ef-dff8-4022-bf8c-bce785bd835e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/989ed7ef-dff8-4022-bf8c-bce785bd835e?resizing_type=fit)
    
6.  Navigate to the **Components** tab, select the **DoorMesh** component.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/dd2c6e48-f119-4d1b-b0a8-11fb92a91f78?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dd2c6e48-f119-4d1b-b0a8-11fb92a91f78?resizing_type=fit)
    
7.  From the **Details** panel change the **Static Mesh** to **SM\_Door**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/c1cb7d28-9899-45fa-acce-030cc2ae6e38?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c1cb7d28-9899-45fa-acce-030cc2ae6e38?resizing_type=fit)
    
8.  Then navigate to the **Transform** category and change the **Y Location** value to **45.0**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/ee0d35ee-d1b3-41d3-ba80-1fa0dbcae1e3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ee0d35ee-d1b3-41d3-ba80-1fa0dbcae1e3?resizing_type=fit)
    
9.  Click **Compile** and **Save** buttons.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/572f6135-0bea-4899-82ee-f3b3e0c0b3ca?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/572f6135-0bea-4899-82ee-f3b3e0c0b3ca?resizing_type=fit)
    

## Creating UCurveFloat and Timeline Event Tracks

The Timeline Component requires a [Timeline Curve](https://dev.epicgames.com/documentation/en-us/unreal-engine/keys-and-curves-in-unreal-engine). Each curve can contain multiple keys that define a time and value.Curves interpolate these keys to calculate the value at any point during the Timeline.

For this example, we will be using a [UCurveFloat](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Curves/UCurveFloat?application_version=5.5).

1.  Navigate to the `ADoorActor` class definition in `DoorActor.h` and declare the following variables:
    
    DoorActor.h
    
    C++
    
    ```code
    `public:          // Variable to hold the Curve asset          UPROPERTY(EditAnywhere)          UCurveFloat* DoorTimelineFloatCurve;       private:          //Float Track Signature to handle our update track event          FOnTimelineFloat UpdateFunctionFloat;           //Function which updates our Door's relative location with the timeline graph`
    
    ```
    
    Expand codeCopy full snippet(12 lines long)
    
2.  Navigate to `DoorActor.cpp` and implement the `UpdateTimelineComp` method:
    
    DoorActor.cpp
    
    C++
    
    `void ADoorActor::UpdateTimelineComp(float Output)      {          // Create and set our Door's new relative location based on the output from our Timeline Curve          FRotator DoorNewRotation = FRotator(0.0f, Output, 0.f);          Door->SetRelativeRotation(DoorNewRotation);      }`
    
    void ADoorActor::UpdateTimelineComp(float Output) { // Create and set our Door&#39;s new relative location based on the output from our Timeline Curve FRotator DoorNewRotation = FRotator(0.0f, Output, 0.f); Door-&gt;SetRelativeRotation(DoorNewRotation); }
    
    Copy full snippet(6 lines long)
    
3.  Then, in the `BeginPlay` method, add the following code:
    
    DoorActor.cpp
    
    C++
    
    `//Binding our float track to our UpdateTimelineComp Function's output      UpdateFunctionFloat.BindDynamic(this, &ADoorActor::UpdateTimelineComp);       //If we have a float curve, bind it's graph to our update function      if (DoorTimelineFloatCurve)      {         DoorTimelineComp->AddInterpFloat(DoorTimelineFloatCurve, UpdateFunctionFloat);      }`
    
    //Binding our float track to our UpdateTimelineComp Function&#39;s output UpdateFunctionFloat.BindDynamic(this, &amp;ADoorActor::UpdateTimelineComp); //If we have a float curve, bind it&#39;s graph to our update function if (DoorTimelineFloatCurve) { DoorTimelineComp-&gt;AddInterpFloat(DoorTimelineFloatCurve, UpdateFunctionFloat); }
    
    Copy full snippet(8 lines long)
    
4.  Compile your code.
    

## Work-In-Progress Code

DoorActor.h

C++

```code
`// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved. 	#pragma once 	#include "Components/TimelineComponent.h" 	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "DoorActor.generated.h"  	UCLASS() 	class TIMELINEDOORACTOR_API ADoorActor : public AActor 	{`

```

Expand codeCopy full snippet(53 lines long)

DoorActor.cpp

C++

```code
`//Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#include "DoorActor.h" 	#include "Components/BoxComponent.h"  	// Sets default values 	ADoorActor::ADoorActor() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;`

```

Expand codeCopy full snippet(51 lines long)

## Creating and Binding Collision Overlap Events

The Box Component requires the ability to react when an Actor enters or leaves its collision bounds.

1.  Navigate to the class definition of your `DoorActor.h` file and declare the following:
    
    DoorActor.h
    
    C++
    
    `// Begin and End Overlap Events for our DoorProxVolume      UFUNCTION()      void OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);       UFUNCTION()      void OnOverlapEnd(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);`
    
    // Begin and End Overlap Events for our DoorProxVolume UFUNCTION() void OnOverlapBegin(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult&amp; SweepResult); UFUNCTION() void OnOverlapEnd(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex);
    
    Copy full snippet(6 lines long)
    
2.  Next, navigate to your `DoorActor.cpp` file to implement your `OnOverlapBegin` and `OnOverlapEnd` class methods:
    
    DoorActor.cpp
    
    C++
    
    `void ADoorActor::OnOverlapBegin(UPrimitiveComponent * OverlappedComp, AActor * OtherActor, UPrimitiveComponent * OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult)      {          DoorTimelineComp->Play();      }       void ADoorActor::OnOverlapEnd(UPrimitiveComponent * OverlappedComp, AActor * OtherActor, UPrimitiveComponent * OtherComp, int32 OtherBodyIndex)      {          DoorTimelineComp->Reverse();      }`
    
    void ADoorActor::OnOverlapBegin(UPrimitiveComponent \* OverlappedComp, AActor \* OtherActor, UPrimitiveComponent \* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult &amp; SweepResult) { DoorTimelineComp-&gt;Play(); } void ADoorActor::OnOverlapEnd(UPrimitiveComponent \* OverlappedComp, AActor \* OtherActor, UPrimitiveComponent \* OtherComp, int32 OtherBodyIndex) { DoorTimelineComp-&gt;Reverse(); }
    
    Copy full snippet(9 lines long)
    
3.  Bind your overlap functions in the `BeginPlay` method, as following:
    
    DoorActor.cpp
    
    C++
    
    ```code
    `void ADoorActor::BeginPlay()      {          Super::BeginPlay();           //Binding our float track to our UpdateTimelineComp Function's output          UpdateFunctionFloat.BindDynamic(this, &ADoorActor::UpdateTimelineComp);           //If we have a float curve, bind it's graph to our update function          if (DoorTimelineFloatCurve)          {`
    
    ```
    
    Expand codeCopy full snippet(17 lines long)
    
4.  Compile your code.
    

## Creating a Curve Asset in the Unreal Editor

You must create a **Curve Asset** in the **Unreal Editor** to assign it to your Timeline Actor Blueprint.

1.  Navigate to the **Content Browser**, select **Add (+) > Miscellaneous > Curve**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/94f94f8c-14e7-4b9f-b71c-3e5d34712d2e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/94f94f8c-14e7-4b9f-b71c-3e5d34712d2e?resizing_type=fit)
    
2.  Select **CurveFloat** and name the Asset **DoorCurveFloat**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/b179ae03-d970-401c-b9c8-9d41b24c0957?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b179ae03-d970-401c-b9c8-9d41b24c0957?resizing_type=fit)
    
3.  Double-click created **DoorCurveFloat** to open the **Timeline Editor**.
    
4.  Add two keys to the Float Curve, by right clicking on the **Graph**, then select **Add Key**. Adjust time-value of the first key to the **(0, 0)**. Adjust time-value of the second key to the **(4, 90)**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/de5198c0-9ecb-4fed-8ffd-f4291a3c5d79?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/de5198c0-9ecb-4fed-8ffd-f4291a3c5d79?resizing_type=fit)
    
    Click image for full size.
    
    For more information on editing **Timeline** curves, see [Keys and Curves](https://dev.epicgames.com/documentation/en-us/unreal-engine/keys-and-curves-in-unreal-engine).
    
5.  Press **Shift** and click to select both your keys, right click on the **Graph** and set them to **Auto** interpolation.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/11d8a328-9b33-43e5-bee1-01180bc2a0a2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/11d8a328-9b33-43e5-bee1-01180bc2a0a2?resizing_type=fit)
    
    Click image for full size.
    
6.  Your Curve now should look as following. Save your **DoorCuveFloat** and close **Timeline Editor**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/efa3df1d-e9fa-42c7-beb7-2c76979fb28c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/efa3df1d-e9fa-42c7-beb7-2c76979fb28c?resizing_type=fit)
    
    Click image for full size.
    
7.  Open your **Bp\_DoorActor** and select the **Bp\_DoorActor** from the **Components** tab.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2fa63d46-d20b-46c6-8fbe-fc3fc0d5e1cb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2fa63d46-d20b-46c6-8fbe-fc3fc0d5e1cb?resizing_type=fit)
    
8.  Navigate to the **Details** panel and select **DoorCurveFloat** from the **Door Timeline Float Curve** dropdown menu of the **Door Action** section.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/4d89235f-3ec6-458f-b7e5-54caa3d2d137?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4d89235f-3ec6-458f-b7e5-54caa3d2d137?resizing_type=fit)
    
9.  Navigate to the **Content Browser** and place the **Bp\_DoorActor** into the **Level**.
    
10.  Compile and Save, then press PIE.
    
    *Using input with WASD, you can control your spectator Pawn. Upon navigating to the collision bounds of your DoorActor, you can observe the timeline play, and upon exiting the bounds, you can observe it play in reverse.*
    

## Finished Code

DoorActor.h

C++

```code
`// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#pragma once 	#include "Components/TimelineComponent.h" 	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "DoorActor.generated.h"  	UCLASS() 	class TIMELINEDOORACTOR_API ADoorActor : public AActor`

```

Expand codeCopy full snippet(61 lines long)

DoorActor.cpp

C++

```code
`// Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#include "DoorActor.h" 	#include "Components/BoxComponent.h"  	// Sets default values 	ADoorActor::ADoorActor() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;`

```

Expand codeCopy full snippet(64 lines long)