# Spawning Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/spawning-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/spawning-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:52

---

## SpawnActor Method

The process of creating a new instance of an **Actor** is known as **spawning**. Spawning of Actors is performed using the `UWorld::SpawnActor()` function. This function creates a new instance of a specified class and returns a pointer to the newly created Actor. `UWorld::SpawnActor()` may only be used for creating instances of classes which inherit from the Actor class in their hierarchy.

```
	`AActor* UWorld::SpawnActor 	( 		UClass*			Class, 		FName			InName, 		FVector const*	Location, 		FRotator const*	Rotation, 		AActor*			Template, 		bool			bNoCollisionFail, 		bool			bRemoteOwned, 		AActor*			Owner, 		APawn*			Instigator, 		bool			bNoFail, 		ULevel*			OverrideLevel, 		bool			bDeferConstruction 	)`

Copy full snippet
```
AActor\* UWorld::SpawnActor ( UClass\* Class, FName InName, FVector const\* Location, FRotator const\* Rotation, AActor\* Template, bool bNoCollisionFail, bool bRemoteOwned, AActor\* Owner, APawn\* Instigator, bool bNoFail, ULevel\* OverrideLevel, bool bDeferConstruction )

| Parameter | Description |
| --- | --- |
| `Class` | A `UClass` specifying the class of the Actor to be spawned. |
| `InName` | (Optional) An `FName` to assign as the `Name` of the Actor being spawned. If no value is specified, the name of the spawned Actor will be automatically generated using the form *\[Class\]\_\[Number\]*. |
| `Location` | (Optional) An `FVector` supplying the initial location to spawn the Actor at. |
| `Rotation` | (Optional) An `FRotator` supplying the initial rotation to spawn the Actor with. |
| `Template` | (Optional) An `AActor` to use as a template when spawning the new Actor. The spawned Actor will be initialized using the property values of the template Actor. If no template Actor is specified, the class default object (CDO) will be used to initialize the spawned Actor. |
| `bNoCollisionFail` | (Optional) A `bool` that determines whether a collision test will be performed when spawning the Actor. If `true`, no collision test will be performed when spawning the Actor regardless of the collision settings of the root component or template Actor. |
| `bRemoteOwned` | (Optional) `bool`. |
| `Owner` | (Optional) The `AActor` that owns the spawned Actor. |
| `Instigator` | (Optional) The `APawn` that is responsible for damage done by the spawned Actor. |
| `bNoFail` | (Optional) A `bool` that determines whether spawning will not fail if certain conditions are not met. If `true`, spawning will not fail because the class being spawned is `bStatic=true` or because the class of the template Actor is not the same as the class of the Actor being spawned. |
| `OverrideLevel` | (Optional) The `ULevel` to spawn the Actor in, i.e. the `Outer` of the Actor. If no level is specified, the `Outer` of the `Owner` is used. If no `Owner` is specified, the persistent level is used. |
| `bDeferConstruction` | (Optional) A `bool` that determines whether the construction script will be run. If `true`, the construction script will not be run on the spawned Actor. Only applicable if the Actor is being spawned from a [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine). |
| **Return Value** |   |
| The spawned Actor in the form of an `AActor` pointer. The return value must be cast to convert to the derived type specified by `Class` parameter. |   |

### Usage

```
	`AKAsset* SpawnedActor1 = (AKAsset*) GetWorld()->SpawnActor(AKAsset::StaticClass(), NAME_None, &Location);`
Copy full snippet
```
AKAsset\* SpawnedActor1 = (AKAsset\*) GetWorld()->SpawnActor(AKAsset::StaticClass(), NAME\_None, &Location);

## Spawn Function Templates

In order to make spawning Actors more friendly, several function templates are provided for the most common usage patterns. These make creating Actors much simpler as they require a smaller subset of parameters and allow the type of the returned Actor to be specified.

### Spawn T Instance, Return T Pointer

This function template spawns an instance of the template class `T` at the same location, and with the same rotation, as the root component of the Actor performing the spawn operation, and returns a pointer to that instance of the same type as the template class, i.e. `T*`. The owning Actor, instigating Pawn, and whether the spawn operation should fail if the spawned Actor encroaches, or would be colliding with another Actor already present in the world can be specified.

```
	`/** Spawns and returns class T, respects default rotation and translation of root component. */ 	template< class T > 	T* SpawnActor 	( 		AActor* Owner=NULL, 		APawn* Instigator=NULL, 		bool bNoCollisionFail=false 	) 	{ 		return (T*)(GetWorld()->SpawnActor(T::StaticClass(), NAME_None, NULL, NULL, NULL, bNoCollisionFail, false, Owner, Instigator)); 	}`
Copy full snippet
```
/\*\* Spawns and returns class T, respects default rotation and translation of root component. \*/ template< class T > T\* SpawnActor ( AActor\* Owner=NULL, APawn\* Instigator=NULL, bool bNoCollisionFail=false ) { return (T\*)(GetWorld()->SpawnActor(T::StaticClass(), NAME\_None, NULL, NULL, NULL, bNoCollisionFail, false, Owner, Instigator)); }

#### Usage

```
	`MyHUD = SpawnActor<AHUD>(this, Instigator);`
Copy full snippet
```
MyHUD = SpawnActor<AHUD>(this, Instigator);

### Spawn T Instance with Transform, Return T Pointer

This function template spawns an instance of the template class `T` at the specified `Location` and with the specified `Rotation`, and returns a pointer to that instance of the same type as the template class, i.e. `T*`. In addition to the location and rotation, the owning Actor, instigating Pawn, and whether the spawn operation should fail if the spawned Actor encroaches, or would be colliding with, another Actor already present in the world can be specified.

```
	`/** Spawns and returns class T, forcibly sets world position. */ 	template< class T > 	T* SpawnActor 	( 		FVector const& Location, 		FRotator const& Rotation, 		AActor* Owner=NULL, 		APawn* Instigator=NULL, 		bool bNoCollisionFail=false 	) 	{ 		return (T*)(GetWorld()->SpawnActor(T::StaticClass(), NAME_None, &Location, &Rotation, NULL, bNoCollisionFail, false, Owner, Instigator)); 	}`
Copy full snippet
```
/\*\* Spawns and returns class T, forcibly sets world position. \*/ template< class T > T\* SpawnActor ( FVector const& Location, FRotator const& Rotation, AActor\* Owner=NULL, APawn\* Instigator=NULL, bool bNoCollisionFail=false ) { return (T\*)(GetWorld()->SpawnActor(T::StaticClass(), NAME\_None, &Location, &Rotation, NULL, bNoCollisionFail, false, Owner, Instigator)); }

#### Usage

```
	`Controller = SpawnActor<AController>(GetLocation(), GetRotation(), NULL, Instigator, true);`
Copy full snippet
```
Controller = SpawnActor<AController>(GetLocation(), GetRotation(), NULL, Instigator, true);

### Spawn Class Instance, Return T Pointer

This function template spawns an instance of the specified `Class` at the same location, and with the same rotation, as the root component of the Actor performing the spawn operation, and returns a pointer to that instance cast to the type of the template class, i.e. `T*`. This requires that the specified `Class` be a child of the template class `T`. In addition to the class, the owning Actor, instigating Pawn, and whether the spawn operation should fail if the spawned Actor encroaches, or would be colliding with, another Actor already present in the world can be specified.

```
	`/** Spawns given class and returns class T pointer, respects default rotation and translation of root component. */ 	template< class T > 	T* SpawnActor 	( 		UClass* Class, 		AActor* Owner=NULL, 		APawn* Instigator=NULL, 		bool bNoCollisionFail=false 	) 	{ 		return (Class != NULL) ? Cast<T>(GetWorld()->SpawnActor(Class, NAME_None, NULL, NULL, NULL, bNoCollisionFail, false, Owner, Instigator)) : NULL; 	}`
Copy full snippet
```
/\*\* Spawns given class and returns class T pointer, respects default rotation and translation of root component. \*/ template< class T > T\* SpawnActor ( UClass\* Class, AActor\* Owner=NULL, APawn\* Instigator=NULL, bool bNoCollisionFail=false ) { return (Class != NULL) ? Cast<T>(GetWorld()->SpawnActor(Class, NAME\_None, NULL, NULL, NULL, bNoCollisionFail, false, Owner, Instigator)) : NULL; }

#### Usage

```
	`MyHUD = SpawnActor<AHUD>(NewHUDClass, this, Instigator);`
Copy full snippet
```
MyHUD = SpawnActor<AHUD>(NewHUDClass, this, Instigator);

### Spawn Class Instance with Transform, Return T Pointer

This function template spawns an instance of the specified `Class` at the specified `Location` and with the specified `Rotation`, and returns a pointer to that instance of the same type as the template class, i.e. `T*`. This requires that the specified `Class` be a child of the template class `T`. In addition to the class, location, and rotation, the owning Actor, instigating Pawn, and whether the spawn operation should fail if the spawned Actor encroaches, or would be colliding with, another Actor already present in the world can be specified.

```
	`/** Spawns given class and returns class T pointer, forcibly sets world position. */ 	template< class T > 	T* SpawnActor 	( 		UClass* Class, 		FVector const& Location, 		FRotator const& Rotation, 		AActor* Owner=NULL, 		APawn* Instigator=NULL, 		bool bNoCollisionFail=false 	) 	{ 		return (Class != NULL) ? Cast<T>(GetWorld()->SpawnActor(Class, NAME_None, &Location, &Rotation, NULL, bNoCollisionFail, false, Owner, Instigator)) : NULL; 	}`
Copy full snippet
```
/\*\* Spawns given class and returns class T pointer, forcibly sets world position. \*/ template< class T > T\* SpawnActor ( UClass\* Class, FVector const& Location, FRotator const& Rotation, AActor\* Owner=NULL, APawn\* Instigator=NULL, bool bNoCollisionFail=false ) { return (Class != NULL) ? Cast<T>(GetWorld()->SpawnActor(Class, NAME\_None, &Location, &Rotation, NULL, bNoCollisionFail, false, Owner, Instigator)) : NULL; }

#### Usage

```
	`APawn* ResultPawn = SpawnActor<APawn>(DefaultPawnClass, StartLocation, StartRotation, NULL, Instigator);`
Copy full snippet
```
APawn\* ResultPawn = SpawnActor<APawn>(DefaultPawnClass, StartLocation, StartRotation, NULL, Instigator);