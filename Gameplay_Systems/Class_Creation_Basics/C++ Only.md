# C++ Only

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cpp-only-example](https://dev.epicgames.com/documentation/en-us/unreal-engine/cpp-only-example)  
**Processed:** 2025-06-14 16:16:28

---

Using the [C++ Class Wizard](/documentation/en-us/unreal-engine/using-the-cplusplus-class-wizard-in-unreal-engine), you can easily add new C++ classes to your project. After you choose the class you would like your new class to derive from, the wizard sets up the necessary header file and source file. If this is the first code you have added to the project, the project is converted to a code project, which creates the game module that contains your source code. It also lets Unreal Editor know that the game module exists, so it can load your C++ changes from Visual Studio or Xcode, and minor code changes can be compiled within Unreal Editor.

The LightSwitch class set up using only C++ is named LightSwitchCodeOnly, and is explained below.

## Class Setup

The **LightSwitchCodeOnly** class was created by using the [C++ Class Wizard](/documentation/en-us/unreal-engine/using-the-cplusplus-class-wizard-in-unreal-engine), and selecting **Actor** as the parent class.

The header file, `LightSwitchCodeOnly.h`, contains the class declaration.

```
	`UCLASS() 	class [PROJECTNAME]_API ALightSwitchCodeOnly : public AActor 	{ 	GENERATED_BODY()  	};`
Copy full snippet
```
UCLASS() class \[PROJECTNAME\]\_API ALightSwitchCodeOnly : public AActor { GENERATED\_BODY() };

Class declarations created with the **C++ Class Wizard** are automatically preceded by the `UCLASS()` macro. The `UCLASS()` macro makes the engine aware of the class, and can also be used with keyword specifiers to set the class's behavior within the engine.

The class declaration contains any variable and/or function declarations. These can be preceded with `UPROPERTY()` and `UFUNCTION()` macros, respectively, which serve similar functions to the `UCLASS()` macro. Components are set up with `UPROPERTY()` macros as well.

In `LightSwitchCodeOnly.h`, C++ is used to:

-   Declare the PointLightComponent and the SphereComponent. The PointLightComponent and the SphereComponent are made `VisibleAnywhere`. This means that their properties will be visible in the **Details** tab of a LightSwitchCodeOnly Actor.
    
    ```
          `public:       /** point light component */       UPROPERTY(VisibleAnywhere, Category = "Switch Components")       class UPointLightComponent* PointLight1; 		       /** sphere component */       UPROPERTY(VisibleAnywhere, Category = "Switch Components")       class USphereComponent* Sphere1;`
    Copy full snippet
    ```
    public: /\*\* point light component \*/ UPROPERTY(VisibleAnywhere, Category = "Switch Components") class UPointLightComponent\* PointLight1; /\*\* sphere component \*/ UPROPERTY(VisibleAnywhere, Category = "Switch Components") class USphereComponent\* Sphere1;
-   Declare your constructor, so you can set default values for your components and variables:
    
    ```
          `ALightSwitchCodeOnly();`
    Copy full snippet
    ```
    ALightSwitchCodeOnly();
-   Declare `OnOverlapBegin` and `OnOverlapEnd`, the functions that will be called when another Actor enters or leaves the SphereComponent. Note that these have different signatures.
    
    ```
          `/** called when something enters the sphere component */       UFUNCTION()       void OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult); 		       /** called when something leaves the sphere component */       UFUNCTION()       void OnOverlapEnd(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);`
    Copy full snippet
    ```
    /\*\* called when something enters the sphere component \*/ UFUNCTION() void OnOverlapBegin(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult); /\*\* called when something leaves the sphere component \*/ UFUNCTION() void OnOverlapEnd(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex);
-   Declare `ToggleLight`, a function that toggles the visibility of the PointLightComponent.
    
    ```
          `/** Toggles the light component's visibility*/       UFUNCTION()       void ToggleLight();`
    Copy full snippet
    ```
    /\*\* Toggles the light component's visibility\*/ UFUNCTION() void ToggleLight();
-   Declare the `DesiredIntensity` variable and make it visible anywhere with the `VisibleAnywhere` specifier. It will show up in the category **Switch Variables** in the **Details** tab of a LightSwitchCodeOnly Actor. For variables that are not subobjects, like this float value, the `VisibleAnywhere` specifier just makes the variable show in the **Details** tab. There is an `EditAnywhere` specifier that can be used as well, but because the `DesiredIntensity` variable is only used right as the Actor is added to the level, the variable does not need to be editable.
    
    ```
          `/** the desired intensity for the light */       UPROPERTY(VisibleAnywhere, Category="Switch Variables")       float DesiredIntensity;`
    Copy full snippet
    ```
    /\*\* the desired intensity for the light \*/ UPROPERTY(VisibleAnywhere, Category="Switch Variables") float DesiredIntensity;

The resulting header file looks like:

LightSwitchCodeOnly.h

```
		`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  		#pragma once  		#include "GameFramework/Actor.h" 		#include "Components/PointLightComponent.h" 		#include "Components/SphereComponent.h" 		#include "LightSwitchCodeOnly.generated.h"  		/** 		 * 		 */ 		UCLASS() 		class [PROJECTNAME]_API ALightSwitchCodeOnly : public AActor 		{ 			GENERATED_BODY() 			public: 			/** point light component */ 			UPROPERTY(VisibleAnywhere, Category = "Switch Components") 			class UPointLightComponent* PointLight1;  			/** sphere component */ 			UPROPERTY(VisibleAnywhere, Category = "Switch Components") 			class USphereComponent* Sphere1;  			ALightSwitchCodeOnly();  			/** called when something enters the sphere component */ 			UFUNCTION() 			void OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);  			/** called when something leaves the sphere component */ 			UFUNCTION() 			void OnOverlapEnd(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);  			/** Toggles the light component's visibility*/ 			UFUNCTION() 			void ToggleLight();  			/** the desired intensity for the light */ 			UPROPERTY(VisibleAnywhere, Category = "Switch Variables") 			float DesiredIntensity;  		};`
Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "GameFramework/Actor.h" #include "Components/PointLightComponent.h" #include "Components/SphereComponent.h" #include "LightSwitchCodeOnly.generated.h" /\*\* \* \*/ UCLASS() class \[PROJECTNAME\]\_API ALightSwitchCodeOnly : public AActor { GENERATED\_BODY() public: /\*\* point light component \*/ UPROPERTY(VisibleAnywhere, Category = "Switch Components") class UPointLightComponent\* PointLight1; /\*\* sphere component \*/ UPROPERTY(VisibleAnywhere, Category = "Switch Components") class USphereComponent\* Sphere1; ALightSwitchCodeOnly(); /\*\* called when something enters the sphere component \*/ UFUNCTION() void OnOverlapBegin(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult); /\*\* called when something leaves the sphere component \*/ UFUNCTION() void OnOverlapEnd(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex); /\*\* Toggles the light component's visibility\*/ UFUNCTION() void ToggleLight(); /\*\* the desired intensity for the light \*/ UPROPERTY(VisibleAnywhere, Category = "Switch Variables") float DesiredIntensity; };

The **C++ Class Wizard** also creates the source file for the class, in this case `LightSwitchCodeOnly.cpp`. By default, the source file has basic includes set up.

You will begin by adding the class constructor.

```
		`ALightSwitchCodeOnly::ALightSwitchCodeOnly() 		{  		}`

Copy full snippet
```
ALightSwitchCodeOnly::ALightSwitchCodeOnly() { }

In the `LightSwitchCodeOnly` constructor, C++ is used to:

-   Set the `DesiredIntensity` variable's value to 3000.
    
    ```
          `DesiredIntensity = 3000.0f;`
    Copy full snippet
    ```
    DesiredIntensity = 3000.0f;
-   Create the PointLightComponent, set its variables (including setting its intensity to the value of `DesiredIntensity`), and make it the root component.
    
    ```
          `PointLight1 = CreateDefaultSubobject<UPointLightComponent>(TEXT("PointLight1"));       PointLight1->Intensity = DesiredIntensity;       PointLight1->SetVisibility(true);       RootComponent = PointLight1;`
    Copy full snippet
    ```
    PointLight1 = CreateDefaultSubobject<UPointLightComponent>(TEXT("PointLight1")); PointLight1->Intensity = DesiredIntensity; PointLight1->SetVisibility(true); RootComponent = PointLight1;
-   Create the SphereComponent, set its variables, and attach it to the PointLightComponent.
    
    ```
          `Sphere1 = CreateDefaultSubobject<USphereComponent>(TEXT("Sphere1"));       Sphere1->InitSphereRadius(250.0f);       Sphere1->SetupAttachment(RootComponent);`
    Copy full snippet
    ```
    Sphere1 = CreateDefaultSubobject<USphereComponent>(TEXT("Sphere1")); Sphere1->InitSphereRadius(250.0f); Sphere1->SetupAttachment(RootComponent);
-   Designate the `OnOverlap` function as a delegate called when an Actor overlaps or leaves the SphereComponent.
    
    ```
          `Sphere1->OnComponentBeginOverlap.AddDynamic(this, &ALightSwitchCodeOnly::OnOverlapBegin);		// set up a notification for when this component overlaps something       Sphere1->OnComponentEndOverlap.AddDynamic(this, &ALightSwitchCodeOnly::OnOverlapEnd);		// set up a notification for when this component overlaps something`
    Copy full snippet
    ```
    Sphere1->OnComponentBeginOverlap.AddDynamic(this, &ALightSwitchCodeOnly::OnOverlapBegin); // set up a notification for when this component overlaps something Sphere1->OnComponentEndOverlap.AddDynamic(this, &ALightSwitchCodeOnly::OnOverlapEnd); // set up a notification for when this component overlaps something

The source file is also where you can define any functions you declared for your class. For instance, `LightSwitchCodeOnly.cpp` has implementations of `OnOverlapBegin` and `OnOverlapEnd`, which toggle the visibility of the PointLightComponent by calling `ToggleLight`. Combined with the class constructor, the source file looks like:

LightSwitchCodeOnly.cpp

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "BasicClasses.h" 	#include "LightSwitchCodeOnly.h"  	ALightSwitchCodeOnly::ALightSwitchCodeOnly() 	{ 		DesiredIntensity = 3000.0f;  		PointLight1 = CreateDefaultSubobject<UPointLightComponent>(TEXT("PointLight1")); 		PointLight1->Intensity = DesiredIntensity; 		PointLight1->SetVisibility(true); 		RootComponent = PointLight1;  		Sphere1 = CreateDefaultSubobject<USphereComponent>(TEXT("Sphere1")); 		Sphere1->InitSphereRadius(250.0f); 		Sphere1->SetupAttachment(RootComponent);  		Sphere1->OnComponentBeginOverlap.AddDynamic(this, &ALightSwitchCodeOnly::OnOverlapBegin);		// set up a notification for when this component overlaps something 		Sphere1->OnComponentEndOverlap.AddDynamic(this, &ALightSwitchCodeOnly::OnOverlapEnd);		// set up a notification for when this component overlaps something  	}  	void ALightSwitchCodeOnly::OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult) 	{ 		if (OtherActor && (OtherActor != this) && OtherComp) 		{ 			ToggleLight(); 		} 	}  	void ALightSwitchCodeOnly::OnOverlapEnd(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex) 	{ 		if (OtherActor && (OtherActor != this) && OtherComp) 		{ 			ToggleLight(); 		} 	}  	void ALightSwitchCodeOnly::ToggleLight() 	{ 		PointLight1->ToggleVisibility(); 	}`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "BasicClasses.h" #include "LightSwitchCodeOnly.h" ALightSwitchCodeOnly::ALightSwitchCodeOnly() { DesiredIntensity = 3000.0f; PointLight1 = CreateDefaultSubobject<UPointLightComponent>(TEXT("PointLight1")); PointLight1->Intensity = DesiredIntensity; PointLight1->SetVisibility(true); RootComponent = PointLight1; Sphere1 = CreateDefaultSubobject<USphereComponent>(TEXT("Sphere1")); Sphere1->InitSphereRadius(250.0f); Sphere1->SetupAttachment(RootComponent); Sphere1->OnComponentBeginOverlap.AddDynamic(this, &ALightSwitchCodeOnly::OnOverlapBegin); // set up a notification for when this component overlaps something Sphere1->OnComponentEndOverlap.AddDynamic(this, &ALightSwitchCodeOnly::OnOverlapEnd); // set up a notification for when this component overlaps something } void ALightSwitchCodeOnly::OnOverlapBegin(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult) { if (OtherActor && (OtherActor != this) && OtherComp) { ToggleLight(); } } void ALightSwitchCodeOnly::OnOverlapEnd(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex) { if (OtherActor && (OtherActor != this) && OtherComp) { ToggleLight(); } } void ALightSwitchCodeOnly::ToggleLight() { PointLight1->ToggleVisibility(); }

`BasicClasses.h` is referring to the name of the project that the class has been set up in.

If this is the first code class you have added to a blank project, you will need to close Unreal Editor, compile the project in Visual Studio or Xcode, and then open Unreal Editor and re-open the project to ensure that the game module is created and loaded properly. Also, it is important to make sure that the **Build Configuration** matches the version of the Unreal Editor executable you are using to open the project. Read more about build configurations and compiling projects in the [Compiling Game Projects](/documentation/en-us/unreal-engine/compiling-game-projects-in-unreal-engine-using-cplusplus) documentation.

If you are adding code to an existing C++ project, you can use the Hot Reload functionality to compile the new code within Unreal Editor.

C++ classes can be extended with C++ classes as well as with Blueprint Classes - they show up after checking the **Show All Classes** checkbox in the **C++ Class Wizard** and in the **Custom Classes** section of the **Pick Parent Class** window during Blueprint Class creation.

The LightSwitchCodeOnly class is in the [Class Viewer](/documentation/en-us/unreal-engine/class-viewer-in-unreal-engine), and can be dragged into the level from there. For more information on placing Actors in a level using the Class Viewer, see the [Placing Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine) documentation.