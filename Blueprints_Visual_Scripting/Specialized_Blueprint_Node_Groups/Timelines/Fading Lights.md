# Fading Lights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fading-lights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fading-lights-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:14

---

Programming Language

×C++

Select an option from the dropdown to see content relevant to it.

This document describes how to set up a light Actor that changes color and slowly fades away on contact.

This will be done using a [Point Light Component](https://dev.epicgames.com/documentation/en-us/unreal-engine/point-lights-in-unreal-engine) containing a Box Component to serve as an overlap trigger and a Timeline component to manipulate the Point Light Actor.

## Creating the Fading Light Actor

1.  Create the new **C++** project based on **Blank** template, name it **FadingLights**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/eccb0c73-253b-49bb-8992-5a0f6680a749?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eccb0c73-253b-49bb-8992-5a0f6680a749?resizing_type=fit)
    
    Click image for full size.
    
2.  Navigate to the **Content Browser**, click **C++ Classes** folder, then click **Add (+)** button and select **New C++ Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/b972f34c-6497-4494-8ac2-e271ee0ec17b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b972f34c-6497-4494-8ac2-e271ee0ec17b?resizing_type=fit)
    
    Click image for full size.
    
3.  Select **Actor** as a **Parent Class**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/54633a02-de33-4b04-9370-36dabac38e10?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/54633a02-de33-4b04-9370-36dabac38e10?resizing_type=fit)
    
    Click image for full size.
    
4.  Name created Actor as **LightActor**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/07ba1cb1-4263-4811-b3a4-78d31aec16f8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/07ba1cb1-4263-4811-b3a4-78d31aec16f8?resizing_type=fit)
    
    Click image for full size.
    
5.  When new Actor is created, **Visual Studio** automatically opens `LightActor.h` and `LightActor.cpp` files. Navigate to the `LightActor.h` file and declare the following:
    
    LightActor.h
    
    C++
    
    `#include "Components/TimelineComponent.h"`
    
    #include &quot;Components/TimelineComponent.h&quot;
    
    Copy full snippet(1 line long)
    
6.  Next, in the `LightActor` class definition, add the following code:
    
    LightActor.h
    
    C++
    
    ```code
    `public:               UPROPERTY(EditAnywhere)              UCurveFloat* PointLightFloatCurve;               UPROPERTY(EditAnywhere)              UCurveLinearColor* PointLightColorCurve;       protected:`
    
    
    ```
    
    Expand codeCopy full snippet(37 lines long)
    
7.  Navigate to `LightActor.cpp` and add the following class libraries.
    
    LightActor.cpp
    
    C++
    
    `#include "Components/BoxComponent.h"      #include "Components/PointLightComponent.h"`
    
    #include &quot;Components/BoxComponent.h&quot; #include &quot;Components/PointLightComponent.h&quot;
    
    Copy full snippet(2 lines long)
    
8.  In the constructor for `ALightActor::ALightActor` declare the following:
    
    LightActor.cpp
    
    C++
    
    ```code
    `ALightActor::ALightActor()      {          // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.          PrimaryActorTick.bCanEverTick = true;           //Create our Default Components          PointLightComp = CreateDefaultSubobject<UPointLightComponent>(TEXT("PointLightComp"));          LightTimelineComp = CreateDefaultSubobject<UTimelineComponent>(TEXT("LightTimelineComp"));          LightOverlapVolume = CreateDefaultSubobject<UBoxComponent>(TEXT("LightOverlapVolume"));`
    
    
    ```
    
    Expand codeCopy full snippet(17 lines long)
    
9.  Next, implement the Point Light component's `UFunction` methods:
    
    LightActor.cpp
    
    C++
    
    `void ALightActor::UpdateLightBrightness(float BrightnessOutput)      {          PointLightComp->SetLightBrightness(BrightnessOutput * 20.0f);      }       void ALightActor::UpdateLightColor(FLinearColor ColorOutput)      {          PointLightComp->SetLightColor(ColorOutput);      }`
    
    void ALightActor::UpdateLightBrightness(float BrightnessOutput) { PointLightComp-&gt;SetLightBrightness(BrightnessOutput \* 20.0f); } void ALightActor::UpdateLightColor(FLinearColor ColorOutput) { PointLightComp-&gt;SetLightColor(ColorOutput); }
    
    Copy full snippet(9 lines long)
    
10.  Then, in the `BeginPlay` method, add the following code:
    
    LightActor.cpp
    
    C++
    
    ```code
    `void ALightActor::BeginPlay()      {          Super::BeginPlay();           //Binding our float and color track to their respective functions          UpdateBrightnessTrack.BindDynamic(this, &ALightActor::UpdateLightBrightness);          UpdateColorTrack.BindDynamic(this, &ALightActor::UpdateLightColor);           //If we have a float curve, bind it's graph to our update function          if (PointLightFloatCurve)`
    
    ```
    
    Expand codeCopy full snippet(20 lines long)
    
11.  Compile your code.
    
12.  From the **Content Browser**, navigate to the **C++ Classes folder**.
    
13.  Right click the **LightActor**, select **Create Blueprint Class based on LightActor**, and name the Blueprint Actor **BP\_LightActor**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/913e8a6e-4b3e-4e32-aec3-2271dd21b7af?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/913e8a6e-4b3e-4e32-aec3-2271dd21b7af?resizing_type=fit)
    

The BP\_LightActor's Class Defaults will appear as they do below:

[![](https://dev.epicgames.com/community/api/documentation/image/6c6b3acd-bc09-4a36-bfbf-6e0704bf7e40?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6c6b3acd-bc09-4a36-bfbf-6e0704bf7e40?resizing_type=fit)

Click image for full size.

## Work-In-Progress Code

LightActor.h

C++

```code
`//Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#pragma once 	#include "Components/TimelineComponent.h" 	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "LightActor.generated.h"  	UCLASS() 	class FADINGLIGHTS_API ALightActor : public AActor`

```

Expand codeCopy full snippet(63 lines long)

LightActor.cpp

C++

```code
`//Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#include "LightActor.h" 	#include "Components/BoxComponent.h" 	#include "Components/PointLightComponent.h"  	// Sets default values 	ALightActor::ALightActor() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.`

```

Expand codeCopy full snippet(63 lines long)

## Creating and Binding the Collision Overlap Event

The Box Component requires the ability to trigger the **TimelineComponent** when an Actor enters its collision bounds.

1.  Navigate to the class definition of the `LightActor.h` file and declare the following under `BrightnessMultiplier`:
    
    LightActor.h
    
    C++
    
    `protected:           UFUNCTION()          void OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);`
    
    protected: UFUNCTION() void OnOverlapBegin(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult&amp; SweepResult);
    
    Copy full snippet(4 lines long)
    
2.  Next, navigate to the `LightActor.cpp` file and implement the `OnOverlapBegin` function.
    
    LightActor.cpp
    
    C++
    
    `void ALightActor::OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult)      {          LightTimelineComp->Play();      }`
    
    void ALightActor::OnOverlapBegin(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult&amp; SweepResult) { LightTimelineComp-&gt;Play(); }
    
    Copy full snippet(4 lines long)
    
3.  Bind the overlap function in the `BeginPlay` method:
    
    LightActor.cpp
    
    C++
    
    `//Binding our Box Component to our Light Actor's Overlap Function      LightOverlapVolume->OnComponentBeginOverlap.AddDynamic(this, &ALightActor::OnOverlapBegin);`
    
    //Binding our Box Component to our Light Actor&#39;s Overlap Function LightOverlapVolume-&gt;OnComponentBeginOverlap.AddDynamic(this, &amp;ALightActor::OnOverlapBegin);
    
    Copy full snippet(2 lines long)
    
4.  Compile your code.
    

## Finished Code

LightActor.h

C++

```code
`//Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	#pragma once 	#include "Components/TimelineComponent.h" 	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "LightActor.generated.h"  	UCLASS() 	class FADINGLIGHTS_API ALightActor : public AActor`

```

Expand codeCopy full snippet(68 lines long)

LightActor.cpp

C++

```code
`//Copyright 1998-2022 Epic Games, Inc. All Rights Reserved.  	// Fill out your copyright notice in the Description page of Project Settings.  	#include "LightActor.h" 	#include "Components/BoxComponent.h" 	#include "Components/PointLightComponent.h"  	// Sets default values 	ALightActor::ALightActor()`

```

Expand codeCopy full snippet(70 lines long)

## Setting Up the Brightness Track

When the player overlaps with the light Actor's box component bounds, the Timeline component will require a float curve to manipulate the Point Light component's brightness value.

The luminosity will have an initial value of **5000** and will decrease to **0** over the span of **5** seconds.

1.  Navigate to the **Content Browser**, select **Add (+) > Miscellaneous > Curve**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/687c5b7f-1f03-4b8d-9af8-168fce9cf379?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/687c5b7f-1f03-4b8d-9af8-168fce9cf379?resizing_type=fit)
    
2.  Select **CurveFloat** and name the Asset **BrightnessCurveFloat**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/182995c7-4d6d-4de2-a172-a0cf6b6faa48?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/182995c7-4d6d-4de2-a172-a0cf6b6faa48?resizing_type=fit)
    
3.  Double-click the **BrightnessCurveFloat** to open the **Timeline Editor**.
    
4.  Add two keys to the Float Curve, by right clicking on the **Graph**, then select **Add Key**. Adjust time-value of the first key to the **(0, 5000)**. Adjust time-value of the second key to the **(5, 0)**. Your **BrightnessCurveFloat** should look as following:
    
    [![](https://dev.epicgames.com/community/api/documentation/image/ffcf364f-6234-4b8e-9127-1a18a4e718d8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ffcf364f-6234-4b8e-9127-1a18a4e718d8?resizing_type=fit)
    
    Click image for full size.
    
5.  Save the **BrightnessCurveFloat**, then navigate back to the **Content Browser** and double-click the **BP\_LightActor** to open its **Class Defaults**.
    
6.  Navigate to the **Details** panel and select **Brightness Curve Float** from the **Point Light Float Curve** dropdown menu.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/bb3657e2-d830-4f2f-841b-aacf0ebcc0dd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bb3657e2-d830-4f2f-841b-aacf0ebcc0dd?resizing_type=fit)
    
7.  Click **Compile** and **Save** buttons.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f92a17c8-6694-447d-9797-58d476e9914e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f92a17c8-6694-447d-9797-58d476e9914e?resizing_type=fit)
    

## Setting Up the Color Track

When the player overlaps with the light Actor's box component bounds, the PointLight Timeline will require a linear color curve track to manipulate the Point Light component's color property.

1.  Navigate to the **Content Browser**, select **Add (+) > Miscellaneous > Curve**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/5f3cfb32-a7cd-4435-b574-e77d8f5497b1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5f3cfb32-a7cd-4435-b574-e77d8f5497b1?resizing_type=fit)
    
2.  Select **CurveLinearColor** and name the asset **LinearColorCurve**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f44ca31d-00cc-405e-afc6-6dbd9a514c6f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f44ca31d-00cc-405e-afc6-6dbd9a514c6f?resizing_type=fit)
    
3.  Double-click the **LinearColorCurve** to open the **Timeline Editor**.
    
4.  Double-click the first color key to modify it, set **RGB** value of: (**R**:1, **G:**0.665, **B**:0.015).
    
    [![](https://dev.epicgames.com/community/api/documentation/image/4e667786-6e4f-433f-8da7-78a0425ab15c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4e667786-6e4f-433f-8da7-78a0425ab15c?resizing_type=fit)
    
    Click image for full size.
    
5.  Double-click the second color key to modify it, set **RGB** value of: (**R**:0, **G:**0, **B**:0).
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f16a3fb6-b808-464b-b34d-90b06955343e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f16a3fb6-b808-464b-b34d-90b06955343e?resizing_type=fit)
    
    Click image for full size.
    
6.  Select second **Point** on the **Graph** by clicking on it and set the time to **5** seconds.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/74991829-98df-4a1b-b070-a104df241083?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/74991829-98df-4a1b-b070-a104df241083?resizing_type=fit)
    
    Click image for full size.
    
7.  Your **LinearColorCurve** should look as following:
    
    [![](https://dev.epicgames.com/community/api/documentation/image/e4ad3c11-1e41-40f9-8615-aeeb2e5f57a3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e4ad3c11-1e41-40f9-8615-aeeb2e5f57a3?resizing_type=fit)
    
    Click image for full size.
    
8.  Save the **LinearColorCurve**, then navigate back to the Content Browser and double-click the **BP\_LightActor** to open its class defaults.
    
9.  Navigate to the **Details Panel** and select **Brightness Curve Float** from the **Point Light Float Curve** dropdown menu.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/5da4ab70-cee2-4934-9a0b-3ce217705013?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5da4ab70-cee2-4934-9a0b-3ce217705013?resizing_type=fit)
    
10.  Click **Compile** and **Save** buttons.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/919826a2-0719-4b17-a180-370287615fcf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/919826a2-0719-4b17-a180-370287615fcf?resizing_type=fit)
    

## Level Setup

To best demonstrate the functionality of the code you have written, you will need to remove all Light Sources Actors from the Level.

1.  In the **Content Browser** navigate to the **BP\_LightActor** Asset, select it and drag it into the **Level**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/0ddf77e3-eb7b-4e4a-800e-c9f791fea353?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0ddf77e3-eb7b-4e4a-800e-c9f791fea353?resizing_type=fit)
    
    Click image for full size.
    
2.  Select the **BP\_LightActor** in the **World Outliner**, navigate to the **Details** panel and set the **Location** settings to **(0, 0, 300)** and the **Scale** settings to **(10, 10, 10)**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2029bc21-e6a2-457b-a006-e75e20a53343?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2029bc21-e6a2-457b-a006-e75e20a53343?resizing_type=fit)
    
3.  Delete the **DirectionalLight Actor** in the **World Outliner**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/71a4986e-bc4a-4c96-849d-40c47cad32a9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/71a4986e-bc4a-4c96-849d-40c47cad32a9?resizing_type=fit)
    
4.  The Level should look as the following.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/c2cb3c7a-c8ed-462a-807f-98bb3d78de16?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c2cb3c7a-c8ed-462a-807f-98bb3d78de16?resizing_type=fit)
    
    Click image for full size.
    

## End Result

Now that the Light Actor and Level have been set up, click **Play (PIE)** to automatically take possession of the spectator Pawn.

You can control the spectator Pawn and navigate into the Light Actor's box component bounds.

Once the Timeline Component's Play function has been triggered, the light's color and luminosity should begin to change over a 5-second timespan.