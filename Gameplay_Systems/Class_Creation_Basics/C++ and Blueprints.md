# C++ and Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cpp-and-blueprints-example](https://dev.epicgames.com/documentation/en-us/unreal-engine/cpp-and-blueprints-example)  
**Processed:** 2025-06-14 16:16:27

---

C++ classes can be extended with Blueprints, allowing programmers to set up new gameplay classes in code that can be built upon and changed with Blueprints by level designers. There are a number of specifiers that change how a C++ class interacts with the Blueprint system, and some of them will be highlighted in this example.

## Class Setup

For the first section of the class setup, a class called LightSwitchBoth is created using the [C++ Class Wizard](/documentation/en-us/unreal-engine/using-the-cplusplus-class-wizard-in-unreal-engine).

Most of the code setup in the LightSwitchBoth class is similar to the code in the [C++ Only LightSwitch example](/documentation/en-us/unreal-engine/cpp-only-example). While you could extend the LightSwitchCodeOnly class with a Blueprint, the components, variables, and functions created in that class would not be accessible to Blueprint graphs. This example will go over the `UPROPERTY()` and `UFUNCTION()` specifiers that make LightSwitchBoth work as a template for the Blueprint that will derive from it.

You may find it helpful to first refer to the C++ Only LightSwitch example, to see how the header file and source file are set up to create the LightSwitchComponent, SphereComponent, DesiredIntensity variable, and OnOverlap function.

This header file is adapted from the C++ Only LightSwitch example to add the following functionality:

-   The PointLightComponent and the SphereComponent are BlueprintReadOnly, and will show up in the category **Switch Components** in the **My Blueprint** tab.
-   OnOverlapBegin and OnOverlapEnd are now BlueprintNativeEvents, and will show up in the category **Switch Functions** in the **My Blueprint** tab.
-   DesiredIntensity is BlueprintReadWrite, and will show up in the category **Switch Variables** in the **My Blueprint** tab.
-   DesiredIntensity is now EditAnywhere instead of VisibleAnywhere.

There is a `Blueprintable` specifier for the `UCLASS()` macro. It is not necessary in this case because LightSwitchBoth inherits directly from Actor, which is Blueprintable, and the Blueprintable specifier is inherited.

With the additional specifiers in the `UPROPERTY()` and `UFUNCTION()` macros, the header file for the LightSwitchBoth class looks like:

LightSwitchBoth.h

```
		`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  		#pragma once  		#include "GameFramework/Actor.h" 		#include "LightSwitchBoth.generated.h"  		/** 		 * 		 */ 		UCLASS() 		class [PROJECTNAME]_API ALightSwitchBoth : public AActor 		{ 			GENERATED_BODY() 			public: 			/** point light component */ 			UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Switch Components") 			class UPointLightComponent* PointLight1;  			/** sphere component */ 			UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Switch Components") 			class USphereComponent* Sphere1;  			ALightSwitchBoth();  			/** called when something enters the sphere component */ 			UFUNCTION(BlueprintNativeEvent, Category="Switch Functions") 			void OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);  			void OnOverlapBegin_Implementation(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);  			/** called when something leaves the sphere component */ 			UFUNCTION(BlueprintNativeEvent, Category="Switch Functions") 			void OnOverlapEnd(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);  			void OnOverlapEnd_Implementation(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);  			/** Toggles the light component's visibility*/ 			UFUNCTION() 			void ToggleLight();  			/** the desired intensity for the light */ 			UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Switch Variables") 			float DesiredIntensity;  		};`
Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "GameFramework/Actor.h" #include "LightSwitchBoth.generated.h" /\*\* \* \*/ UCLASS() class \[PROJECTNAME\]\_API ALightSwitchBoth : public AActor { GENERATED\_BODY() public: /\*\* point light component \*/ UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Switch Components") class UPointLightComponent\* PointLight1; /\*\* sphere component \*/ UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category="Switch Components") class USphereComponent\* Sphere1; ALightSwitchBoth(); /\*\* called when something enters the sphere component \*/ UFUNCTION(BlueprintNativeEvent, Category="Switch Functions") void OnOverlapBegin(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult); void OnOverlapBegin\_Implementation(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult); /\*\* called when something leaves the sphere component \*/ UFUNCTION(BlueprintNativeEvent, Category="Switch Functions") void OnOverlapEnd(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex); void OnOverlapEnd\_Implementation(class UPrimitiveComponent\* OverlappedComp, class AActor\* OtherActor, class UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex); /\*\* Toggles the light component's visibility\*/ UFUNCTION() void ToggleLight(); /\*\* the desired intensity for the light \*/ UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Switch Variables") float DesiredIntensity; };

In the source file for LightSwitchBoth, the constructor remains the same. However, a change needs to be made to the `OnOverlapBegin` and `OnOverlapEnd` functions. These functions are now a BlueprintNativeEvent. This means that in a Blueprint derived from this class, events can be placed that override `OnOverlapBegin` and `OnOverlapEnd`, and are executed when the function would normally be called.

If one of those events does not exist, the C++ implementation of the function executes instead. To make this setup work, the C++ functions need to be renamed `OnOverlapBegin_Implementation` and `OnOverlapEnd_Implementation`, respectively. The Blueprint setup will be covered later in this example.

With the change to the `OnOverlapBegin` and `OnOverlapEnd` definitions, the source file for LightSwitchBoth looks like:

LightSwitchBoth.cpp

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "BasicClasses.h" 	#include "LightSwitchBoth.h"  	ALightSwitchBoth::ALightSwitchBoth() 	{  		DesiredIntensity = 3000.0f;  		PointLight1 = CreateDefaultSubobject<UPointLightComponent>(TEXT("PointLight1")); 		PointLight1->Intensity = DesiredIntensity; 		PointLight1->bVisible = true; 		RootComponent = PointLight1;  		Sphere1 = CreateDefaultSubobject<USphereComponent>(this, TEXT("Sphere1")); 		Sphere1->InitSphereRadius(250.0f); 		Sphere1->SetupAttachment(RootComponent);  		Sphere1->OnComponentBeginOverlap.AddDynamic(this, &ALightSwitchBoth::OnOverlapBegin);		// set up a notification for when this component overlaps something 		Sphere1->OnComponentEndOverlap.AddDynamic(this, &ALightSwitchBoth::OnOverlapEnd);		// set up a notification for when this component overlaps something 	}  	void ALightSwitchBoth::OnOverlapBegin_Implementation(UPrimitiveComponent* OverlappedComp, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult) 	{ 		if (OtherActor && (OtherActor != this) && OtherComp) 		{ 			ToggleLight(); 		} 	}  	void ALightSwitchBoth::OnOverlapEnd_Implementation(UPrimitiveComponent* OverlappedComp, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex) 	{ 		if (OtherActor && (OtherActor != this) && OtherComp) 		{ 			ToggleLight(); 		} 	}  	void ALightSwitchBoth::ToggleLight() 	{ 		PointLight1->ToggleVisibility(); 	}`
Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "BasicClasses.h" #include "LightSwitchBoth.h" ALightSwitchBoth::ALightSwitchBoth() { DesiredIntensity = 3000.0f; PointLight1 = CreateDefaultSubobject<UPointLightComponent>(TEXT("PointLight1")); PointLight1->Intensity = DesiredIntensity; PointLight1->bVisible = true; RootComponent = PointLight1; Sphere1 = CreateDefaultSubobject<USphereComponent>(this, TEXT("Sphere1")); Sphere1->InitSphereRadius(250.0f); Sphere1->SetupAttachment(RootComponent); Sphere1->OnComponentBeginOverlap.AddDynamic(this, &ALightSwitchBoth::OnOverlapBegin); // set up a notification for when this component overlaps something Sphere1->OnComponentEndOverlap.AddDynamic(this, &ALightSwitchBoth::OnOverlapEnd); // set up a notification for when this component overlaps something } void ALightSwitchBoth::OnOverlapBegin\_Implementation(UPrimitiveComponent\* OverlappedComp, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult) { if (OtherActor && (OtherActor != this) && OtherComp) { ToggleLight(); } } void ALightSwitchBoth::OnOverlapEnd\_Implementation(UPrimitiveComponent\* OverlappedComp, AActor\* OtherActor, UPrimitiveComponent\* OtherComp, int32 OtherBodyIndex) { if (OtherActor && (OtherActor != this) && OtherComp) { ToggleLight(); } } void ALightSwitchBoth::ToggleLight() { PointLight1->ToggleVisibility(); }

If this is the first code class you have added to a blank project, you need to close Unreal Editor, compile the project in Visual Studio or Xcode, and then open Unreal Editor and re-open the project to ensure that the game module is created and loaded properly. Also, it is important to make sure that the **Build Configuration** matches the version of the Unreal Editor executable you are using to open the project. Read more about build configurations and compiling projects in the [Compiling Game Projects](/documentation/en-us/unreal-engine/compiling-game-projects-in-unreal-engine-using-cplusplus) documentation.

If you are adding code to an existing C++ project, you can use the Hot Reload functionality to compile the new code within Unreal Editor.

After compiling this new class, it is possible to [create](/documentation/en-us/unreal-engine/creating-blueprint-classes-in-unreal-engine) a new [Blueprint Class](/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine). In this case, LightSwitchBoth is chosen as the parent class for the Blueprint, which will be named **LightSwitchBoth\_BP**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17404efd-7bdd-403d-a860-54cc886ca3cb/bpboth_parentclass.png)

The PointLightComponent and SphereComponent added in C++ also show in the **Components** tab in the **Blueprint Editor**. Their icons are dark blue to indicate that they are native components, inherited from the parent LightSwitchBoth class. Any new components added just to the **LightSwitchBoth\_BP** Blueprint would have light blue icons instead. To learn more about adding and arranging components using the **Components** tab, refer to the [Components](/documentation/en-us/unreal-engine/components-window-in-unreal-engine) tab documentation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99599b49-dbe9-45de-85fd-382f1e16e97d/both_componentlist.png)

The **Blueprint Editor**'s **Graph** panel is the core of Blueprint editing. In the **Graph** panel, you can add new [variables](/documentation/en-us/unreal-engine/blueprint-variables-in-unreal-engine), [functions](/documentation/en-us/unreal-engine/functions-in-unreal-engine), and [macros](/documentation/en-us/unreal-engine/macros-in-unreal-engine) in the [Blueprint Editor My Blueprint Panel](/documentation/en-us/unreal-engine/my-blueprint-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine) tab. You also have access to all the [graphs](/documentation/en-us/unreal-engine/graphs-in-unreal-engine) contained within the Blueprint Class. In graphs, [nodes](/documentation/en-us/unreal-engine/nodes-in-unreal-engine) are wired together to create design-time and gameplay functionality that can be driven by class variables, gameplay events,and even an Actor's surroundings.

The **My Blueprint** tab in the **Graph** panel displays the PointLightComponent and the SphereComponent added in C++ to the LightSwitchBoth class. This is because of the `BlueprintReadOnly` specifier. Nodes for these components can be added to a graph by clicking and dragging from their names in the **My Blueprint** tab into the graph. These nodes can then be connected to nodes that change variables like visibility or light color. The **DesiredIntensity** variable also appears in the **My Blueprint** tab. Because it is a variable and not a component, the `BlueprintReadWrite` specifier can be used. This means it is possible to create nodes to both get and set the value of **DesiredIntensity** in a Blueprint graph. Refer to the [Blueprint Editor My Blueprint Panel](/documentation/en-us/unreal-engine/my-blueprint-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine) documentation for general usage information.

The components and variables from the parent LightSwitchBoth class might not display by default. The **Show inherited variables** checkbox at the bottom of the **My Blueprint** tab shows variables inherited from the parent class when checked.

| Showing All Variables | Showing Only User-Created Variables |
| --- | --- |
| 
![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f159789-c7c6-49b4-9e5f-d52581051087/showinhvar2.png)

 | 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/580f98d3-b5bc-48f8-a118-bc8be3e18a02/showinhvar.png)

 |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/298600d2-49b2-486a-9223-3812740a3cf4/bp_only_myblueprint.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b3e89c1-0c7f-4ad9-947d-bc0b382f914a/both_myblueprint.png) |

There are two graphs used to set up the LightSwitchBoth\_BP class behavior. The first is the [Construction Script](/documentation/en-us/unreal-engine/construction-script-in-unreal-engine) graph, which contains a specialized Construction Script event. Without the Construction Script setup, a new LightSwitchBoth\_BP Actor would just use the LightSwitchBoth constructor. However, the Construction Script executes when the Actor is moved within the level, as well as when DesiredIntensity is changed. Using the Construction Script means that Actor variables exposed to Blueprints can be changed easily and the effects of these changes can be seen quickly.

In the **LightSwitchBoth\_BP** class, the **Construction Script** event is connected to a **Set Intensity** node, so that the brightness of **Point Light 1** (the PointLightComponent) is set to the value of **DesiredIntensity** when the Actor is added to or moved within the level or DesiredIntensity changes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ee7ec66-25f0-40d1-91cd-14756c9febd6/both_constructionscript.png)

The other graph set up in the LightSwitch\_BPOnly class is the [EventGraph](/documentation/en-us/unreal-engine/event-graph-in-unreal-engine). Execution in the EventGraph begins from events. In this case, the OnOverlap event executes whenever the C++ function `OnOverlap` would be called. In the LightSwitchBoth source file, delegates were setup so OnOverlap will execute when an Actor enters or leaves the SphereComponent:

```
		`Sphere1->OnComponentBeginOverlap.AddDynamic(this, &ALightSwitchBoth::OnOverlapBegin);		// set up a notification for when this component overlaps something 		Sphere1->OnComponentEndOverlap.AddDynamic(this, &ALightSwitchBoth::OnOverlapEnd);		// set up a notification for when this component overlaps something`

Copy full snippet
```
Sphere1->OnComponentBeginOverlap.AddDynamic(this, &ALightSwitchBoth::OnOverlapBegin); // set up a notification for when this component overlaps something Sphere1->OnComponentEndOverlap.AddDynamic(this, &ALightSwitchBoth::OnOverlapEnd); // set up a notification for when this component overlaps something

The **OnOverlap** event node is connected to a **Set Light Color** node. Whenever the event executes, it will cause the light color of the PointLightComponent to be set to a random color. This overrides the `OnOverlap_Implementation` function in the source file, which toggles the visibility of the PointLightComponent.

For more on events and working with graphs, refer to the [Events](/documentation/en-us/unreal-engine/events-in-unreal-engine), [EventGraph](/documentation/en-us/unreal-engine/event-graph-in-unreal-engine), and [Blueprint Class UI](/documentation/en-us/unreal-engine/blueprints-visual-scripting-user-interface-for-blueprint-classes-in-unreal-engine) documentation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f0e3b06-54b5-4d26-8d9d-5263900b6925/both_eventgraph_2.png)

The **DesiredIntensity** variable is set to EditAnywhere in the LightSwitchBoth header file, so it is visible in the **Blueprint Editor**'s Defaults and can be edited by clicking the **Class Defaults** button to show the Class Defaults in the Details Panel. This also means that the variable can be changed for each instance of the class, so each Actor can have its own DesiredIntensity. Because DesiredIntensity is also BlueprintReadWrite and used in the Construction Script, updating it also causes the Construction Script to execute again.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c8dd3e7-86d6-4e5c-a260-7bbc90f8e513/both_defaults.png)

Blueprinted classes can be extended with other Blueprint Classes, either using the dropdown button next to the class in the **Class Viewer** to create a new Blueprint, or by **Right-clicking** on the Blueprint and selecting **Create New Blueprint Based on This**.

The Blueprint Class LightSwitchBoth\_BP is in the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine), and can be dragged into the level from there. It is also in the [Class Viewer](/documentation/en-us/unreal-engine/class-viewer-in-unreal-engine). For more information on placing Actors in a level using the Content Browser or Class Viewer, refer to the [Placing Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine) documentation.