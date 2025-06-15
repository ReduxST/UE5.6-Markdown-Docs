# Programming Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-cpp-quick-start](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-cpp-quick-start)  
**Processed:** 2025-06-14 16:56:35

---

Windows macOS Linux ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/243b6458-a67d-496c-a97d-e964aa16bb69/programmingquickstarttopic.png)

In this Quick Start Guide, you will learn how to set up a C++ project in the Unreal Engine and program your first C++ gameplay class in Visual Studio. By the time you've completed this tutorial, you will know how to do the following:

-   Create a new C++ Project
-   Create a new Actor class in C++
-   Edit that C++ class in your development environment, adding visual representation and functionality
-   Compile your project
-   Test your new Actor in the Unreal Editor

This guide assumes that you have already set up Visual Studio as your programming environment. If not, please refer to [Setting Up Visual Studio for the Unreal Engine](/documentation/404) for instructions on how to install it and get it set up for programming with the Unreal Engine. We also assume that you have some familiarity with using the **Unreal Editor** before starting this guide, but for your convenience we will walk through all the steps necessary to create and manage C++ classes from the editor. The end product of this guide will be a cube that floats softly in mid-air and continually rotates, giving you a simple object to test as you learn to use the development environment for programming.

This guide assumes that you have already set up XCode as your programming environment. We also assume that you have some familiarity with using the **Unreal Editor** before starting this guide, but for your convenience we will walk through all the steps necessary to create and manage C++ classes from the editor. The end product of this guide will be a cube that floats softly in mid-air and continually rotates, giving you a simple object to test as you learn to use the development environment for programming.

## 1\. Required Setup

Launch the **Unreal Editor**. When the **Project Browser** comes up, click **Games** Project category and select a **Blank** template. Make sure that you have **C++** and **Starter Content** enabled, choose your preferred **Save Location** and **Name** for this project, and then click **Create Project**. In our instance, we're naming our project QuickStart.

This will automatically create a simple, blank project with only essential C++ code in the solution, and it will automatically open inside both the Unreal Editor and Visual Studio. For more information on managing and creating Projects, please refer to the [Project Browser](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) page.

This will automatically create a simple, blank project with only essential C++ code in the solution, and it will automatically open inside both the Unreal Editor and XCode. For more information on managing and creating Projects, please refer to the [Project Browser](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) page.

Any Blueprint project can be converted to a C++ project. If you have a Blueprint project that you want to add C++ to, create a new C++ class per the next section, and the editor will set up your code environment for you. Also note that using a C++ project does not prevent you from using Blueprint. C++ projects simply set up the base classes for your project in C++ instead of Blueprint.

## 2\. Create a New C++ Class

1.  In the **Unreal Editor**, click the **File** drop-down menu, then select the **New C++ Class...** command.
    
    Click image for full size.
    
2.  The **Choose Parent Class** menu will display. You can choose an existing class to extend, adding its functionality to your own. Choose **Actor**, as it is the most basic type of object that can be placed in the world, then click **Next**.
    
    Click image for full size.
    
3.  In the **Name Your New Actor** menu, name your Actor **FloatingActor** and click **Create Class**.
    
    Click image for full size.
    
    The Unreal Engine will automatically compile and reload with our new class selected in the Content Browser, and your programming environment will automatically open with `FloatingActor.cpp`.
    

## 3\. Edit Your C++ Class

Now that we have created our C++ Class, we're going to switch over to Visual Studio and edit our code.

1.  In **Visual Studio**, locate the **Solution Explorer**, which by default is on the left side of the window, then use it to locate `FloatingActor.h`. In our project, it will be located under **Games > QuickStart > Source > QuickStart**.
    
    ![Solution Explorer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6134e843-6347-492e-9123-2cc3c9d1dce7/prquickstart_3-1.png)
2.  Double-click `FloatingActor.h` to open it and bring it into focus in the text editor.
    
    ![Open Header File](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dec8c07-c71a-47b8-8f9d-0a90b03d71ac/prquickstart_3-2.png)
    
    This is a *header* file. You can think of it as being sort of like a table of contents for a C++ class. Before we can start building any new functionality, we must declare any new **Variables** or **Functions** that we're using in this file.
    
3.  Add the following code underneath the declaration for **AFloatingActor()**:
    
    ```
             `UPROPERTY(VisibleAnywhere)          UStaticMeshComponent* VisualMesh;`
    		
    Copy full snippet
    ```
    UPROPERTY(VisibleAnywhere) UStaticMeshComponent\* VisualMesh;
    
    Here we're declaring a **StaticMeshComponent**, which will act as our visual representation for our object. Note that it uses a **UProperty** macro, which makes it visible inside the Unreal Editor. For more information on UProperty and its specifiers, see the page on [Properties](/documentation/en-us/unreal-engine/unreal-engine-uproperties).
    
4.  Now open `FloatingActor.cpp` and add the following code inside of **AFloatingActor::AFloatingActor()**, just before the closing bracket:
    
    ```
             `VisualMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh"));          VisualMesh->SetupAttachment(RootComponent); 		          static ConstructorHelpers::FObjectFinder<UStaticMesh> CubeVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape_Cube.Shape_Cube")); 		          if (CubeVisualAsset.Succeeded())          {              VisualMesh->SetStaticMesh(CubeVisualAsset.Object);              VisualMesh->SetRelativeLocation(FVector(0.0f, 0.0f, 0.0f));          }`
    		
    Copy full snippet
    ```
    VisualMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh")); VisualMesh->SetupAttachment(RootComponent); static ConstructorHelpers::FObjectFinder<UStaticMesh> CubeVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape\_Cube.Shape\_Cube")); if (CubeVisualAsset.Succeeded()) { VisualMesh->SetStaticMesh(CubeVisualAsset.Object); VisualMesh->SetRelativeLocation(FVector(0.0f, 0.0f, 0.0f)); }
    
    This function is the *constructor*, and it tells the class how to initialize itself when it is first created. The code we have added will fill our VisualMesh reference in with a new StaticMeshComponent, attach it to our Actor, and set it to the cube mesh from the **Starter Content** assets. For more information about attaching components in code, refer to our guide for [Creating and Attaching Components](/documentation/en-us/unreal-engine/quick-start-guide-to-components-and-collision-in-unreal-engine-cpp).
    
5.  Add the following code inside of **AFloatingActor::Tick(float DeltaTime)**, just before the closing bracket:
    
    ```
             `FVector NewLocation = GetActorLocation();          FRotator NewRotation = GetActorRotation();          float RunningTime = GetGameTimeSinceCreation();          float DeltaHeight = (FMath::Sin(RunningTime + DeltaTime) - FMath::Sin(RunningTime));          NewLocation.Z += DeltaHeight * 20.0f;       //Scale our height by a factor of 20          float DeltaRotation = DeltaTime * 20.0f;	//Rotate by 20 degrees per second          NewRotation.Yaw += DeltaRotation;          SetActorLocationAndRotation(NewLocation, NewRotation);`
    		
    Copy full snippet
    ```
    FVector NewLocation = GetActorLocation(); FRotator NewRotation = GetActorRotation(); float RunningTime = GetGameTimeSinceCreation(); float DeltaHeight = (FMath::Sin(RunningTime + DeltaTime) - FMath::Sin(RunningTime)); NewLocation.Z += DeltaHeight \* 20.0f; //Scale our height by a factor of 20 float DeltaRotation = DeltaTime \* 20.0f; //Rotate by 20 degrees per second NewRotation.Yaw += DeltaRotation; SetActorLocationAndRotation(NewLocation, NewRotation);
    
    The **Tick** function is where we add code that we want to execute in real-time. In this case, it will make our cube simultaneously rotate while also floating up and down. For more information about Ticking actors, see [Actor Ticking](/documentation/en-us/unreal-engine/actor-ticking-in-unreal-engine).
    

Now that we have created our C++ Class, we're going to switch over to XCode and edit our code.

1.  In **XCode**, locate the **Project Navigator**, which by default is on the left side of the window, then use it to locate `FloatingActor.h`. In our project, it will be located under **Games > QuickStart > Source > QuickStart**.
    
    ![Solution Explorer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/affef541-126d-4d7a-b8a3-04398f3f0f9f/prquickstart_mac_3-1.png)
2.  Double-click `FloatingActor.h` to open it and bring it into focus in the text editor. This is a *header* file. You can think of it as a table of contents for a C++ class. Before we can start building any new functionality, we must declare any new **Variables** or **Functions** that we're using in this file.
    
3.  Add the following code underneath the declaration for **AFloatingActor()**:
    
    ```
             `UPROPERTY(VisibleAnywhere)          UStaticMeshComponent* VisualMesh;`
    		
    Copy full snippet
    ```
    UPROPERTY(VisibleAnywhere) UStaticMeshComponent\* VisualMesh;
    
    Here we're declaring a **StaticMeshComponent**, which will act as our visual representation for our object. Note that it uses a **UProperty** macro, which makes it visible inside the Unreal Editor. For more information on UProperty and its specifiers, see the page on [Properties](/documentation/en-us/unreal-engine/unreal-engine-uproperties).
    
4.  Now open `FloatingActor.cpp` and add the following code inside of **AFloatingActor::AFloatingActor()**, just before the closing bracket:
    
    ```
             `VisualMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh"));          VisualMesh->SetupAttachment(RootComponent); 		          static ConstructorHelpers::FObjectFinder<UStaticMesh> CubeVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape_Cube.Shape_Cube")); 		          if (CubeVisualAsset.Succeeded())          {              VisualMesh->SetStaticMesh(CubeVisualAsset.Object);              VisualMesh->SetRelativeLocation(FVector(0.0f, 0.0f, 0.0f));          }`
    		
    Copy full snippet
    ```
    VisualMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh")); VisualMesh->SetupAttachment(RootComponent); static ConstructorHelpers::FObjectFinder<UStaticMesh> CubeVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape\_Cube.Shape\_Cube")); if (CubeVisualAsset.Succeeded()) { VisualMesh->SetStaticMesh(CubeVisualAsset.Object); VisualMesh->SetRelativeLocation(FVector(0.0f, 0.0f, 0.0f)); }
    
    This function is the *constructor*, and it tells the class how to initialize itself when it is first created. The code we have added will fill our VisualMesh reference in with a new StaticMeshComponent, attach it to our Actor, and set it to the cube mesh from the **Starter Content** assets. For more information about attaching components in code, refer to our guide for [Creating and Attaching Components](/documentation/en-us/unreal-engine/quick-start-guide-to-components-and-collision-in-unreal-engine-cpp).
    
5.  Add the following code inside of **AFloatingActor::Tick(float DeltaTime)**, just before the closing bracket:
    
    ```
             `FVector NewLocation = GetActorLocation();          FRotator NewRotation = GetActorRotation();          float RunningTime = GetGameTimeSinceCreation();          float DeltaHeight = (FMath::Sin(RunningTime + DeltaTime) - FMath::Sin(RunningTime));          NewLocation.Z += DeltaHeight * 20.0f;       //Scale our height by a factor of 20          float DeltaRotation = DeltaTime * 20.0f;	//Rotate by 20 degrees per second          NewRotation.Yaw += DeltaRotation;          SetActorLocationAndRotation(NewLocation, NewRotation);`
    		
    Copy full snippet
    ```
    FVector NewLocation = GetActorLocation(); FRotator NewRotation = GetActorRotation(); float RunningTime = GetGameTimeSinceCreation(); float DeltaHeight = (FMath::Sin(RunningTime + DeltaTime) - FMath::Sin(RunningTime)); NewLocation.Z += DeltaHeight \* 20.0f; //Scale our height by a factor of 20 float DeltaRotation = DeltaTime \* 20.0f; //Rotate by 20 degrees per second NewRotation.Yaw += DeltaRotation; SetActorLocationAndRotation(NewLocation, NewRotation);
    
    The **Tick** function is where we add code that we want to execute in real-time. In this case, it will make our cube simultaneously rotate while also floating up and down. For more information about Ticking actors, see [Actor Ticking](/documentation/en-us/unreal-engine/actor-ticking-in-unreal-engine).
    

## 4\. Compile and Test Your C++ Code

1.  **Save** your work in both `FloatingActor.h` and `FloatingActor.cpp`. Then, in the **Solution Explorer**, right-click the project, click the **Build** command in the context menu, and wait for the project to finish compiling.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8174624d-99a6-4c53-b92f-f0d6242b794b/prquickstart_4-1.png)
    
    You should see a message that says "Succeeded" in the **Output** log at the bottom of the window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dbcb626-dec8-4cf5-a56d-b67de5f253c4/prquickstart_4-2.png)
    
    Alternatively, you can go back to the **Unreal Editor** and click the **Compile** button in the toolbar at the top of the screen.
    

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0947de55-2ec1-4a97-8a6f-0b2689a15f6e/prquickstart_4-3.png)

You should always save your work before attempting to compile, otherwise the changes you make in your code will not take effect.

1.  In the **Unreal Editor**, go back to the **Content Browser**, unfold **C++ Classes**, and then locate **FloatingActor**. It will be located in the folder that has the same name as your project, in our case, QuickStart.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25b68feb-f2b6-40b1-b222-0a10dea3b041/prquickstart_4-4.png)
2.  Click and drag **FloatingActor** into the **Perspective Viewport** to create an instance of FloatingActor. It will be selected in the **World Outliner** as "FloatingActor1" and its properties will be visible in the **Details Panel**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80a661c7-2a87-4dd6-838b-562a3f964532/prquickstart_4-5.png)
    
    For more information about navigating the Viewport and placing Actors in the World, refer to the [Level Designer Quick Start](/documentation/en-us/unreal-engine/level-designer-quick-start-in-unreal-engine).
    
3.  In the **Details Panel** for **FloatingActor1**, set your Actor's **Location** to (-180, 0, 180). This will place it directly over the table in the default scene.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5aa2d0de-69c9-4886-ba36-767ae9bf8db2/prquickstart_4-6.png)
    
    Alternatively, you can use the Move gizmo to move it there manually.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19abe77d-14a7-42c8-af8f-956aeff1b04f/prquickstart_4-7.png)
4.  Press the **Play In Editor** button at the top of the screen.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d3a6147-e012-4ac0-85aa-ebffe6066fb6/prquickstart_4-8.png)

1.  **Save** your work in both `FloatingActor.h` and `FloatingActor.cpp`. Then, click the **Product** drop-down menu at the top of the screen, select the **Build** command, and wait for the project to finish building.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03d24e7d-4513-4275-89f3-a51dd537b549/prquickstart_mac_4-1.png)
    
    You should see a message that says "Succeeded" in the **Output** log at the bottom of the window. Alternatively, you can go back to the **Unreal Editor** and click the **Compile** button in the toolbar at the top of the screen.
    

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d95f3199-7d15-4e32-bbe3-4a6d33bba2b6/prquickstart_4-3.png)

You should always save your work before attempting to compile, otherwise the changes you make in your code will not take effect.

1.  In the **Unreal Editor**, go back to the **Content Browser**, unfold **C++ Classes**, and then locate **FloatingActor**. It will be located in the folder that has the same name as your project, in our case, QuickStart.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f79ad05-81e0-44be-941f-8b1698b6223a/prquickstart_4-4.png)
2.  Click and drag **FloatingActor** into the **Perspective Viewport** to create an instance of FloatingActor. It will be selected in the **World Outliner** as "FloatingActor1" and its properties will be visible in the **Details Panel**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e50303b8-a80a-4128-b1a2-ab18aaf09b52/prquickstart_4-5.png)
    
    For more information about navigating the Viewport and placing Actors in the World, refer to the [Level Designer Quick Start](/documentation/en-us/unreal-engine/level-designer-quick-start-in-unreal-engine).
    
3.  In the **Details Panel** for **FloatingActor1**, set your Actor's **Location** to (-180, 0, 180). This will place it directly over the table in the default scene.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe7c4419-c31f-4e23-ac0e-0dc25aa6b911/prquickstart_4-6.png)
    
    Alternatively, you can use the Move gizmo to move it there manually.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e03fa52-1529-49ff-a739-6cafba673fdb/prquickstart_4-7.png)
4.  Press the **Play In Editor** button at the top of the screen.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8af09ee-40b9-4cdf-ae4c-24b3e02ad8b6/prquickstart_4-8.png)

## 5\. End Result

You should now see your cube gently floating up and down over the table while it slowly rotates.

Congratulations! You've created your first Actor class entirely with C++! While this represents a very simple object and only scratches the surface of what you can do with C++ source code, you have at this point touched on all the essentials of creating, editing, and compiling C++ code for your game. You are now ready for more complex gameplay programming challenges, and we suggest a few below.

## 6\. On Your Own!

Now that you know how to build a simple C++ Actor, try making it more configurable. For instance, you can add variables to control its behavior:

In **FloatingActor.h**:

```
	`... 	public: 		UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="FloatingActor") 		float FloatSpeed = 20.0f;  		UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="FloatingActor") 		float RotationSpeed = 20.0f; 	...`

Copy full snippet
```
... public: UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="FloatingActor") float FloatSpeed = 20.0f; UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="FloatingActor") float RotationSpeed = 20.0f; ...

In **FloatingActor.cpp**:

```
	`... 	NewLocation.Z += DeltaHeight * FloatSpeed;			//Scale our height by FloatSpeed 	float DeltaRotation = DeltaTime * RotationSpeed;	//Rotate by a number of degrees equal to RotationSpeed each second 	...`

Copy full snippet
```
... NewLocation.Z += DeltaHeight \* FloatSpeed; //Scale our height by FloatSpeed float DeltaRotation = DeltaTime \* RotationSpeed; //Rotate by a number of degrees equal to RotationSpeed each second ...

By adding these variables in the header and replacing the float values we were using to scale DeltaHeight and DeltaRotation in the .cpp, we can now edit the float and rotation speed in the **Details Panel** when we select our Actor.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6358f21b-e9e5-4d60-b3db-f42f2c023e8c/prquickstart_6-1.png)

You can experiment by adding other kinds of behavior to the Tick function using Location, Rotation, and Scale.

You can also try attaching other kinds of components in C++ to create a more complex object. Refer to the [Creating and Attaching Components](/documentation/en-us/unreal-engine/quick-start-guide-to-components-and-collision-in-unreal-engine-cpp) guide for examples of different types of components you have available, and try adding a Particle System Component to add a bit of flare to your floating object.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e16e673-276e-4b89-b99a-95d7cfa39288/prquickstart_6-2.png)

Finally, if you right-click your own Actor class in the **Content Browser**, you will find the option to extend it, either in C++ or in Blueprint, enabling you to create new variations of it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9ec935b-a8a9-430c-b0ee-141b897c5d8c/prquickstart_6-3.png)

You can have a whole library of FloatingActors, each substituting different Meshes or parameters as you so choose.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d02b5f8e-6d2e-41ba-b33f-d9124c96cb59/prquickstart_6-4.png)

## Sample Code

**FloatingActor.h**

```
	`// Copyright 1998-2019 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Actor.h" 	#include "FloatingActor.generated.h"  	UCLASS() 	class QUICKSTART_API AFloatingActor : public AActor 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this actor's properties 		AFloatingActor();  		UPROPERTY(VisibleAnywhere) 		UStaticMeshComponent* VisualMesh;  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick(float DeltaTime) override;  	};`

Copy full snippet
```
// Copyright 1998-2019 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Actor.h" #include "FloatingActor.generated.h" UCLASS() class QUICKSTART\_API AFloatingActor : public AActor { GENERATED\_BODY() public: // Sets default values for this actor's properties AFloatingActor(); UPROPERTY(VisibleAnywhere) UStaticMeshComponent\* VisualMesh; protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick(float DeltaTime) override; };

**FloatingActor.cpp**

```
	`// Copyright 1998-2019 Epic Games, Inc. All Rights Reserved.  	#include "FloatingActor.h"  	// Sets default values 	AFloatingActor::AFloatingActor() 	{ 		// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		VisualMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh")); 		VisualMesh->SetupAttachment(RootComponent);  		static ConstructorHelpers::FObjectFinder<UStaticMesh> CubeVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape_Cube.Shape_Cube"));  		if (CubeVisualAsset.Succeeded()) 		{ 			VisualMesh->SetStaticMesh(CubeVisualAsset.Object); 			VisualMesh->SetRelativeLocation(FVector(0.0f, 0.0f, 0.0f)); 		} 	}  	// Called when the game starts or when spawned 	void AFloatingActor::BeginPlay() 	{ 		Super::BeginPlay();  	}  	// Called every frame 	void AFloatingActor::Tick(float DeltaTime) 	{ 		Super::Tick(DeltaTime);  		FVector NewLocation = GetActorLocation(); 		FRotator NewRotation = GetActorRotation(); 		float RunningTime = GetGameTimeSinceCreation(); 		float DeltaHeight = (FMath::Sin(RunningTime + DeltaTime) - FMath::Sin(RunningTime)); 		NewLocation.Z += DeltaHeight * 20.0f;       //Scale our height by a factor of 20 		float DeltaRotation = DeltaTime * 20.0f;	//Rotate by 20 degrees per second 		NewRotation.Yaw += DeltaRotation; 		SetActorLocationAndRotation(NewLocation, NewRotation); 	}`
Copy full snippet
```
// Copyright 1998-2019 Epic Games, Inc. All Rights Reserved. #include "FloatingActor.h" // Sets default values AFloatingActor::AFloatingActor() { // Set this actor to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; VisualMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh")); VisualMesh->SetupAttachment(RootComponent); static ConstructorHelpers::FObjectFinder<UStaticMesh> CubeVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape\_Cube.Shape\_Cube")); if (CubeVisualAsset.Succeeded()) { VisualMesh->SetStaticMesh(CubeVisualAsset.Object); VisualMesh->SetRelativeLocation(FVector(0.0f, 0.0f, 0.0f)); } } // Called when the game starts or when spawned void AFloatingActor::BeginPlay() { Super::BeginPlay(); } // Called every frame void AFloatingActor::Tick(float DeltaTime) { Super::Tick(DeltaTime); FVector NewLocation = GetActorLocation(); FRotator NewRotation = GetActorRotation(); float RunningTime = GetGameTimeSinceCreation(); float DeltaHeight = (FMath::Sin(RunningTime + DeltaTime) - FMath::Sin(RunningTime)); NewLocation.Z += DeltaHeight \* 20.0f; //Scale our height by a factor of 20 float DeltaRotation = DeltaTime \* 20.0f; //Rotate by 20 degrees per second NewRotation.Yaw += DeltaRotation; SetActorLocationAndRotation(NewLocation, NewRotation); }