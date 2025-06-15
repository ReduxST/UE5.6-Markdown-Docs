# Creating Gameplay in Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-gameplay-in-unreal-engine-for-unity-developers](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-gameplay-in-unreal-engine-for-unity-developers)  
**Processed:** 2025-06-14 16:17:31

---

This page explains Unreal Engine (UE) gameplay programming concepts for Unity users. The explanations below assume you are familiar with Unity C# and want to learn UE C++ and Blueprint.

The examples below cover some common gameplay programming use cases in Unity C# and how to implement the same functionality in UE.

## Instantiating GameObject / Spawning Actor

In Unity, you use the `Instantiate` function to create new instances of objects. This function takes any `UnityEngine.Object` type (GameObject, MonoBehaviour, etc.), and makes a copy of it.

C#

`public GameObject EnemyPrefab; public Vector3 SpawnPosition; public Quaternion SpawnRotation;  void Start() { 	GameObject NewGO = (GameObject)Instantiate(EnemyPrefab, SpawnPosition, SpawnRotation); 	NewGO.name = "MyNewGameObject"; }`

public GameObject EnemyPrefab; public Vector3 SpawnPosition; public Quaternion SpawnRotation; void Start() { GameObject NewGO = (GameObject)Instantiate(EnemyPrefab, SpawnPosition, SpawnRotation); NewGO.name = "MyNewGameObject"; }

Copy full snippet(9 lines long)

UE has two different functions to instantiate objects:

-   `NewObject` creates new `UObject` types.
    
-   `SpawnActor` spawns `AActor` types.
    

### UObjects and NewObject

Subclassing `UObject` in UE is similar to subclassing `ScriptableObject` in Unity. These are useful for gameplay classes that do not need to spawn into the world or have attached components as Actors do.

In Unity, if you created a subclass of `ScriptableObject`, you can instantiate it like this:

C#

`MyScriptableObject NewSO = ScriptableObject.CreateInstance<MyScriptableObject>();`

MyScriptableObject NewSO = ScriptableObject.CreateInstance<MyScriptableObject>();

Copy full snippet(1 line long)

In UE, if you create a subclass of `UObject`, you can instantiate it like this:

C++

`UMyObject* NewObj = NewObject<UMyObject>();`

UMyObject\* NewObj = NewObject<UMyObject>();

Copy full snippet(1 line long)

### AActors and SpawnActor

You can spawn Actors using the `SpawnActor` method on a World (`UWorld` in C++) object. Some UObjects and all Actors provide a `GetWorld` method to get the World object.

In the example below, we use those methods with an existing Actor's spawn parameters to emulate the functionality of Unity's `Instantiate` method.

#### Example

Below is the example AActor subclass, `AMyActor`. The default constructor initializes the `int32` and `USphereComponent*`.

Note the use of the `CreateDefaultSubobject` function. This function creates Components and assigns default properties to them. Sub-objects created with this function act as a default template, so you can modify them in a subclass or Blueprint.

C++

```code
`UCLASS() class AMyActor : public AActor { 	GENERATED_BODY()  	UPROPERTY() 	int32 MyIntProp;  	UPROPERTY() 	USphereComponent* MyCollisionComp;`

```

Expand codeCopy full snippet(20 lines long)

This creates a clone of a `AMyActor`, including all member variables, UPROPERTYs, and Components.

C++

`AMyActor* CreateCloneOfMyActor(AMyActor* ExistingActor, FVector SpawnLocation, FRotator SpawnRotation) { 	UWorld* World = ExistingActor->GetWorld(); 	FActorSpawnParameters SpawnParams; 	SpawnParams.Template = ExistingActor; 	World->SpawnActor<AMyActor>(ExistingActor->GetClass(), SpawnLocation, SpawnRotation, SpawnParams); }`

AMyActor\* CreateCloneOfMyActor(AMyActor\* ExistingActor, FVector SpawnLocation, FRotator SpawnRotation) { UWorld\* World = ExistingActor->GetWorld(); FActorSpawnParameters SpawnParams; SpawnParams.Template = ExistingActor; World->SpawnActor<AMyActor>(ExistingActor->GetClass(), SpawnLocation, SpawnRotation, SpawnParams); }

Copy full snippet(7 lines long)

## Casting from One Type to Another

In this case, we get a component we know we have, then cast it to a specific type and conditionally do something.

#### Unity

C#

`Collider collider = gameObject.GetComponent<Collider>; SphereCollider sphereCollider = collider as SphereCollider; if (sphereCollider != null) { 		// ... }`

Collider collider = gameObject.GetComponent<Collider>; SphereCollider sphereCollider = collider as SphereCollider; if (sphereCollider != null) { // ... }

Copy full snippet(6 lines long)

#### UE C++

C++

`UPrimitiveComponent* Primitive = MyActor->GetComponentByClass(UPrimitiveComponent::StaticClass()); USphereComponent* SphereCollider = Cast<USphereComponent>(Primitive); if (SphereCollider != nullptr) { 		// ... }`

UPrimitiveComponent\* Primitive = MyActor->GetComponentByClass(UPrimitiveComponent::StaticClass()); USphereComponent\* SphereCollider = Cast<USphereComponent>(Primitive); if (SphereCollider != nullptr) { // ... }

Copy full snippet(6 lines long)

#### Blueprint

You can cast in Blueprint by using a **Cast to** node. For more detailed information, see [Casting Quick Start Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/casting-quick-start-guide-in-unreal-engine).

## Destroying GameObject / Actor

|  |  |  |
| --- | --- | --- |
| 
**Unity C#**

C#

`Destroy(MyGameObject);`

Destroy(MyGameObject);

Copy full snippet(1 line long)

 | 

**UE C++**

C++

`MyActor->Destroy();`

MyActor->Destroy();

Copy full snippet(1 line long)

 | 

**Blueprint**

[![](https://dev.epicgames.com/community/api/documentation/image/fb7488ae-917d-4d70-815c-670b453f3aa1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fb7488ae-917d-4d70-815c-670b453f3aa1?resizing_type=fit)



 |

## Destroying GameObject / Actor (with 1-Second Delay)

|  |  |  |
| --- | --- | --- |
| 
**Unity C#**

C#

`Destroy(MyGameObject, 1);`

Destroy(MyGameObject, 1);

Copy full snippet(1 line long)

 | 

**UE C++**

C++

`MyActor->SetLifeSpan(1);`

MyActor->SetLifeSpan(1);

Copy full snippet(1 line long)

 | 

**Blueprint**

[![](https://dev.epicgames.com/community/api/documentation/image/01009987-7e14-4e3c-aeb8-9b7b6440cd81?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/01009987-7e14-4e3c-aeb8-9b7b6440cd81?resizing_type=fit)



 |

## Disabling GameObjects / Actors

|  |  |  |
| --- | --- | --- |
| 
**Unity C#**

C#

`MyGameObject.SetActive(false);`

MyGameObject.SetActive(false);

Copy full snippet(1 line long)

 | 

**UE C++**

C++

`// Hides visible components MyActor->SetActorHiddenInGame(true);  // Disables collision components MyActor->SetActorEnableCollision(false);  // Stops the Actor from ticking MyActor->SetActorTickEnabled(false);`

// Hides visible components MyActor->SetActorHiddenInGame(true); // Disables collision components MyActor->SetActorEnableCollision(false); // Stops the Actor from ticking MyActor->SetActorTickEnabled(false);

Copy full snippet(8 lines long)

 | 

**Blueprint**

[![](https://dev.epicgames.com/community/api/documentation/image/689707f7-b239-4c44-b508-176cc366d5ba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/689707f7-b239-4c44-b508-176cc366d5ba?resizing_type=fit)



 |

## Accessing the GameObject / Actor from a Component

|  |  |  |
| --- | --- | --- |
| 
**Unity C#**

C++

`GameObject ParentGO = MyComponent.gameObject;`

GameObject ParentGO = MyComponent.gameObject;

Copy full snippet(2 lines long)

 | 

**UE C++**

C++

`AActor* ParentActor = MyComponent->GetOwner();`

AActor\* ParentActor = MyComponent->GetOwner();

Copy full snippet(2 lines long)

 | 

**Blueprint**

[![](https://dev.epicgames.com/community/api/documentation/image/71a31ef3-bbac-4c45-a80c-47e6dd51d0da?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/71a31ef3-bbac-4c45-a80c-47e6dd51d0da?resizing_type=fit)



 |

## Accessing a Component from the GameObject / Actor

#### Unity

C#

`MyComponent MyComp = gameObject.GetComponent<MyComponent>();`

MyComponent MyComp = gameObject.GetComponent<MyComponent>();

Copy full snippet(1 line long)

#### UE C++

C++

`UMyComponent* MyComp = MyActor->FindComponentByClass<UMyComponent>();`

UMyComponent\* MyComp = MyActor->FindComponentByClass<UMyComponent>();

Copy full snippet(1 line long)

#### Blueprint

[![](https://dev.epicgames.com/community/api/documentation/image/c5db4405-f52e-4d87-ac7c-042b50f408b7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c5db4405-f52e-4d87-ac7c-042b50f408b7?resizing_type=fit)

## Finding GameObjects / Actors

#### Unity

C#

```code
`// Find GameObject by name GameObject MyGO = GameObject.Find("MyNamedGameObject");  // Find Objects by type MyComponent[] Components = Object.FindObjectsOfType(typeof(MyComponent)) as MyComponent[]; foreach (MyComponent Component in Components) { 		// ... }`


```

Expand codeCopy full snippet(16 lines long)

#### UE C++

C++

```code
`// Find UObjects by type for (TObjectIterator<UMyObject> It; It; ++it) { 	UMyObject* MyObject = *It; 	// ... }  // Find Actor by name (also works on UObjects) AActor* MyActor = FindObject<AActor>(nullptr, TEXT("MyNamedActor"));`


```

Expand codeCopy full snippet(26 lines long)

#### Blueprint

[![](https://dev.epicgames.com/community/api/documentation/image/68b9a54e-e28e-493a-9752-459ccf84a1f8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/68b9a54e-e28e-493a-9752-459ccf84a1f8?resizing_type=fit)

[![](https://dev.epicgames.com/community/api/documentation/image/9b61fae8-2c7b-44ee-b8f4-177ec88d94b1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9b61fae8-2c7b-44ee-b8f4-177ec88d94b1?resizing_type=fit)

## Adding Tags to GameObjects / Actors

#### Unity

C#

`MyGameObject.tag = "MyTag";`

MyGameObject.tag = "MyTag";

Copy full snippet(1 line long)

#### UE C++

C++

`// Actors can have multiple tags MyActor.Tags.AddUnique(TEXT("MyTag"));`

// Actors can have multiple tags MyActor.Tags.AddUnique(TEXT("MyTag"));

Copy full snippet(2 lines long)

#### Blueprint

[![](https://dev.epicgames.com/community/api/documentation/image/26918efc-0d14-4aec-b8df-d9958cb268c3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/26918efc-0d14-4aec-b8df-d9958cb268c3?resizing_type=fit)

## Adding Tags to MonoBehaviours / ActorComponents

#### Unity

C#

`// This changes the tag on the GameObject it is attached to MyComponent.tag = "MyTag";`

// This changes the tag on the GameObject it is attached to MyComponent.tag = "MyTag";

Copy full snippet(2 lines long)

#### UE C++

C++

`// Components have their own array of tags MyComponent.ComponentTags.AddUnique(TEXT("MyTag"));`

// Components have their own array of tags MyComponent.ComponentTags.AddUnique(TEXT("MyTag"));

Copy full snippet(2 lines long)

## Comparing Tags on GameObjects / Actors and MonoBehaviours / ActorComponents

#### Unity

C#

`if (MyGameObject.CompareTag("MyTag")) { 	// ... }  // Checks the tag on the GameObject it is attached to if (MyComponent.CompareTag("MyTag")) { 	// ... }`

if (MyGameObject.CompareTag("MyTag")) { // ... } // Checks the tag on the GameObject it is attached to if (MyComponent.CompareTag("MyTag")) { // ... }

Copy full snippet(10 lines long)

#### UE C++

C++

`// Checks if an Actor has this tag if (MyActor->ActorHasTag(FName(TEXT("MyTag")))) { 	// ... }`

// Checks if an Actor has this tag if (MyActor->ActorHasTag(FName(TEXT("MyTag")))) { // ... }

Copy full snippet(5 lines long)

#### Blueprint

[![](https://dev.epicgames.com/community/api/documentation/image/4384de8d-5bc9-4875-80df-4ff4d3911c1a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4384de8d-5bc9-4875-80df-4ff4d3911c1a?resizing_type=fit)

#### UE C++

C++

`// Checks if an ActorComponent has this tag if (MyComponent->ComponentHasTag(FName(TEXT("MyTag")))) { 	// ... }`

// Checks if an ActorComponent has this tag if (MyComponent->ComponentHasTag(FName(TEXT("MyTag")))) { // ... }

Copy full snippet(5 lines long)

#### Blueprint

[![](https://dev.epicgames.com/community/api/documentation/image/0c722b70-f411-4419-8998-660157690933?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0c722b70-f411-4419-8998-660157690933?resizing_type=fit)

## Physics: RigidBody vs. Primitive Component

In Unity, to give a GameObject physics characteristics, you attach a RigidBody component.

In UE, any Primitive Component (`UPrimitiveComponent` in C++) can represent a physical object. Some common Primitive Components are:

-   Shape Components (`USphereComponent`, `UCapsuleComponent`, etc.)
    
-   Static Mesh Components
    
-   Skeletal Mesh Components
    

Unlike Unity, which separates the responsibilities of collision and visualizations into separate components, UE combines the concepts of "potentially physical" and "potentially visible" into a single Primitive Component. Any Component with geometry in the world that can be rendered or physically interacted with is a subclass of `UPrimitiveComponent`.

Collision Channels are the UE equivalent of layers in Unity. To learn more, refer to [Collision Filtering](https://www.unrealengine.com/en-US/blog/collision-filtering).

### RayCast vs. RayTrace

#### Unity

C#

```code
`GameObject FindGOCameraIsLookingAt() { 	Vector3 Start = Camera.main.transform.position; 	Vector3 Direction = Camera.main.transform.forward; 	float Distance = 100.0f; 	int LayerBitMask = 1 << LayerMask.NameToLayer("Pawn");  	RaycastHit Hit; 	bool bHit = Physics.Raycast(Start, Direction, out Hit, Distance, LayerBitMask);`


```

Expand codeCopy full snippet(17 lines long)

#### UE C++

C++

```code
`APawn* AMyPlayerController::FindPawnCameraIsLookingAt() { 	// You can use this to customize various properties about the trace 	FCollisionQueryParams Params; 	// Ignore the player's pawn 	Params.AddIgnoredActor(GetPawn());  	// The hit result gets populated by the line trace 	FHitResult Hit;`


```

Expand codeCopy full snippet(23 lines long)

#### Blueprint

[![](https://dev.epicgames.com/community/api/documentation/image/c5c26aa0-10b0-4e48-8220-5c29bd8b5d11?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c5c26aa0-10b0-4e48-8220-5c29bd8b5d11?resizing_type=fit)

Click the image for full size.

### Trigger Volumes

#### Unity

C#

```code
`public class MyComponent : MonoBehaviour { 	void Start() 	{ 		collider.isTrigger = true; 	} 	void OnTriggerEnter(Collider Other) 	{ 		// ... 	}`

```

Expand codeCopy full snippet(15 lines long)

#### UE C++

C++

```code
`UCLASS() class AMyActor : public AActor { 	GENERATED_BODY()  	// My trigger component 	UPROPERTY() 	UPrimitiveComponent* Trigger;  	AMyActor()`

```

Expand codeCopy full snippet(25 lines long)

#### Blueprint

[![](https://dev.epicgames.com/community/api/documentation/image/b9ddaf52-9b15-48d4-bc8b-3670d4e31452?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b9ddaf52-9b15-48d4-bc8b-3670d4e31452?resizing_type=fit)

To learn more about setting up collision responses, see [Collision](https://dev.epicgames.com/documentation/en-us/unreal-engine/collision-in-unreal-engine).

### Kinematic Rigidbodies

#### Unity

C#

`public class MyComponent : MonoBehaviour { 	void Start() 	{ 		rigidbody.isKinematic = true; 		rigidbody.velocity = transform.forward * 10.0f; 	} }`

public class MyComponent : MonoBehaviour { void Start() { rigidbody.isKinematic = true; rigidbody.velocity = transform.forward \* 10.0f; } }

Copy full snippet(8 lines long)

#### UE C++

C++

```code
`UCLASS() class AMyActor : public AActor { 	GENERATED_BODY()  	UPROPERTY() 	UPrimitiveComponent* PhysicalComp;  	AMyActor() 	{`

```

Expand codeCopy full snippet(15 lines long)

## Input Events

#### Unity

C#

```code
`public class MyPlayerController : MonoBehaviour { 	void Update() 	{ 		if (Input.GetButtonDown("Fire")) 		{ 			// ... 		} 		float Horiz = Input.GetAxis("Horizontal"); 		float Vert = Input.GetAxis("Vertical");`

```

Expand codeCopy full snippet(13 lines long)

#### UE C++

C++

```code
`UCLASS() class AMyPlayerController : public APlayerController { 	GENERATED_BODY()  	void SetupInputComponent() 	{ 		Super::SetupInputComponent();  		InputComponent->BindAction("Fire", IE_Pressed, this, &AMyPlayerController::HandleFireInputEvent);`

```

Expand codeCopy full snippet(18 lines long)

#### Blueprint

[![](https://dev.epicgames.com/community/api/documentation/image/15504e00-984c-41e9-9db8-d1c5414b03d1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/15504e00-984c-41e9-9db8-d1c5414b03d1?resizing_type=fit)

This is what your input properties in your Project Settings might look like:

[![Input settings in Unreal Engine](https://dev.epicgames.com/community/api/documentation/image/7b31af9c-d644-47ba-94d0-a6fa414d6d49?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7b31af9c-d644-47ba-94d0-a6fa414d6d49?resizing_type=fit)

To learn more about how to set up input for your UE project, see [Input](https://dev.epicgames.com/documentation/en-us/unreal-engine/input-in-unreal-engine).

## Further Reading

For more information related to the concepts above, we recommend that you review the following sections:

-   [Gameplay Framework](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine) - Covers core game systems such as game mode, player state, controllers, pawns, cameras, and more.
    
-   [Gameplay Architecture](https://dev.epicgames.com/documentation/en-us/unreal-engine/programming-with-cpp-in-unreal-engine) - Reference for creating and implementing gameplay classes.
    
-   [Gameplay Tutorials](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-tutorials-for-unreal-engine) - Tutorials for recreating common gameplay elements.