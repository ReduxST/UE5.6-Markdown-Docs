# UObject Instance Creation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-objects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-objects-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:40

---

## NewObject

`NewObject()` is the simplest UObject factory method. It takes in an optional outer object and class and creates a new instance with an automatically generated name.

```
	`template< class T > 	T* NewObject 	( 		UObject* Outer=(UObject*)GetTransientPackage(), 		UClass* Class=T::StaticClass() 	)`
Copy full snippet
```
template< class T > T\* NewObject ( UObject\* Outer=(UObject\*)GetTransientPackage(), UClass\* Class=T::StaticClass() )

| Parameter | Description |
| --- | --- |
| `Outer` | (Optional) A `UObject` to set as the Outer for the Object being created. |
| `Class` | (Optional) A `UClass` specifying the class of the Object to be created. |
| **Return Value** | A pointer to the spawned instance of the specified class. |

## NewNamedObject

`NewNamedObject()` expands on `NewObject()` by allowing a name for the new instance as well as [Object Flags](/documentation/en-us/unreal-engine/creating-objects-in-unreal-engine#objectflags) and a template object to be specified as an argument.

```
	`template< class TClass > 	TClass* NewNamedObject 	( 		UObject* Outer, 		FName Name, 		EObjectFlags Flags = RF_NoFlags, 		UObject const* Template=NULL 	)`
Copy full snippet
```
template< class TClass > TClass\* NewNamedObject ( UObject\* Outer, FName Name, EObjectFlags Flags = RF\_NoFlags, UObject const\* Template=NULL )

| Parameter | Description |
| --- | --- |
| `Outer` | A `UObject` to set as the Outer for the Object being created. |
| `Name` | An `FName` to set as the `Name` for the new Object. |
| `Flags` | (Optional) An `FObjectFlags` enum value describing the new Object. |
| `Template` | (Optional) A `UObject` to use as a template when creating the new Object. |
| **Return Value** | A pointer to the spawned instance of the specified class. |

## ConstructObject

For complete flexibility, new instances of `UObjects` can be created using the `ConstructObject()` function. This function calls `StaticConstructObject()`, which allocates the Object, executes the `ClassConstructor`, and performs any initialization such as loading config properties, loading localized properties, and instancing components.

```
	`template< class T > 	T* ConstructObject 	( 		UClass* Class, 		UObject* Outer = (UObject*)GetTransientPackage(), 		FName Name=NAME_None, 		EObjectFlags SetFlags=RF_NoFlags, 		UObject const* Template=NULL, 		bool bCopyTransientsFromClassDefaults=false, 		struct FObjectInstancingGraph* InstanceGraph=NULL 	)`
Copy full snippet
```
template< class T > T\* ConstructObject ( UClass\* Class, UObject\* Outer = (UObject\*)GetTransientPackage(), FName Name=NAME\_None, EObjectFlags SetFlags=RF\_NoFlags, UObject const\* Template=NULL, bool bCopyTransientsFromClassDefaults=false, struct FObjectInstancingGraph\* InstanceGraph=NULL )

| Parameter | Description |
| --- | --- |
| `Class` | A `UClass` specifying the class of the Object to be created. |
| `Outer` | (Optional) A `UObject` to set as the Outer for the Object being created. |
| `Name` | (Optional) An `FName` to set as the `Name` for the new Object. |
| `SetFlags` | (Optional) An `EObjectFlags` enum value describing the new Object. |
| `Template` | (Optional) A `UObject` to use as a template when creating the new Object. |
| `bCopyTransientsFromClassDefaults` | (Optional) A `bool` that determines whether to copy transient properties from the class default object instead of the passed-in archetype pointer. If `true`, the class default object's transients are used. |
| `FObjectInstancingGraph` | (Optional) An `FObjectInstancingGraph` struct that contains the mappings of instanced objects and components to their templates. Used when for instancing components owned by the new Object. |
| **Return Value** | A pointer to the spawned instance of the specified class. |

## Object Flags

The `EObjectFlags` enumeration is used to quickly and succinctly describe an Object. There are various flags to describe the type of Object, how it is handled by garbage collection, the stage the Object is at in its lifetime, etc. There are also special all or none masks and predefined groups of flags.

| Flag | Value | Description |
| --- | --- | --- |
| **Object Type** |   |   |
| RF\_Public | `0x00000001` | The Object is visible outside of the package it is contained within. |
| RF\_Standalone | `0x00000002` | The Object is kept around for editing even if is not referenced by anything. |
| RF\_Native | `0x00000004` | The Objectis native. This is only used for `UClass` objects. |
| RF\_Transactional | `0x00000008` | The Object is transactional. |
| RF\_ClassDefaultObject | `0x00000010` | The Object is the default object for its class, i.e. the default template that new instances of that class use when being created. |
| RF\_ArchetypeObject | `0x00000020` | The Object is a template for another object. It is treated like a class default object. |
| RF\_Transient | `0x00000040` | The Object is not saved to disk. |
| **Garbage Collection** |   |   |
| RF\_RootSet | `0x00000080` | The Object is not garbage collected even if it is not referenced by anything. |
| RF\_IsLazyReferenced | `0x00000100` | The Object is referenced by a lazy pointer and requires additional cleanup upon deletion. |
| RF\_Unreachable | `0x00000200` | The Object is not reachable on the object graph. |
| RF\_TagGarbageTemp | `0x00000400` | The Object is marked for use by various utilities that use garbage collection. This flag is not interpreted by the garbage collector itself. |
| **Object Lifetime** |   |   |
| RF\_NeedLoad | `0x00000800` | The Object needs loading. |
| RF\_AsyncLoading | `0x00001000` | The Object is being loaded asynchronously. |
| RF\_NeedPostLoad | `0x00002000` | The Object needs to be post-loaded. |
| RF\_NeedPostLoadSubobjects | `0x00004000` | The Object still needs to instance sub-objects and fix up serialized component references |
| RF\_PendingKill | `0x00008000` | The Object is pending destruction. Marks the Object as being invalid for gameplay purposes, but still a valid Object. |
| RF\_BeginDestroyed | `0x00010000` | The Object has had `BeginDestroy()` called on it. |
| RF\_FinishDestroyed | `0x00020000` | The Object has had `FinishDestroy()` called on it. |
| **Special Masks** |   |   |
| RF\_AllFlags | `0x0003ffff` | The Object has all flags. Used mainly for error checking. |
| RF\_NoFlags | `0x00000000` | The Object has no flags. Used to avoid a cast. |
| **Predefined Groups** |   |   |
| RF\_Load | 
`RF_Public | RF_Standalone | RF_Native | RF_Transactional | RF_ClassDefaultObject | RF_ArchetypeObject`



 | Flags loaded from Unreal files. |
| RF\_PropagateToSubobjects | 

`RF_Public | RF_ArchetypeObject | RF_Transactional`



 | Flags inherited by sub-objects from their super-objects. |