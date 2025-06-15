# Unreal Engine Reflection System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reflection-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/reflection-system-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:13

---

The **Unreal Engine Reflection System** encapsulates your classes with various macros that provide engine and editor functionality. When programming with **Unreal Engine**(**UE**), it is possible to have standard C++ classes, functions, and variables.

-   The base class for objects in Unreal is [UObject](/documentation/en-us/unreal-engine/objects-in-unreal-engine). Each class defines a template for a new [Actor](/documentation/en-us/unreal-engine/actors-in-unreal-engine) or Object.
    
-   You can use the `UCLASS` macro to tag classes derived from `UObject` so that the [UObject handling system](/documentation/en-us/unreal-engine/unreal-object-handling-in-unreal-engine) is aware of them.
    
-   [TSubclassOf](/documentation/en-us/unreal-engine/typed-object-pointer-properties-in-unreal-engine) is a template class that provides `UClass` type safety. It is useful for assigning classes that derive from a specific type. For example, you may expose this variable to Blueprint where a designer can assign which weapon class is spawned for a Player Character.
    
-   Classes can contain [structs](/documentation/en-us/unreal-engine/structs-in-unreal-engine). Structs are data structures that help with the organization and manipulation of their related member properties. Structs can be defined on their own using the `USTRUCT()` macro.
    
-   The [Unreal Smart Pointer Library](/documentation/en-us/unreal-engine/smart-pointers-in-unreal-engine) is a custom implementation of C++11 smart pointers designed to ease the burden of memory allocation and tracking. This implementation includes the industry standard [Shared Pointers](/documentation/en-us/unreal-engine/shared-pointers-in-unreal-engine), [Weak Pointers](/documentation/en-us/unreal-engine/weak-pointers-in-unreal-engine), **Unique Pointers**, and [Shared References](/documentation/en-us/unreal-engine/shared-references-in-unreal-engine) which act like non-nullable Shared Pointers.
    
-   [Interfaces](/documentation/en-us/unreal-engine/interfaces-in-unreal-engine) provide functions and additional gameplay behavior you can implement in multiple or different classes. Your player character can interact with a variety of Actors in the world. Each of these interactions can cause a different reaction to an event.
    
-   [Metadata Specifiers](/documentation/en-us/unreal-engine/metadata-specifiers-in-unreal-engine) control how classes, interfaces, structs, enums, functions, or properties interact with various aspects of the engine and editor. Each type of data structure or member has its own list of Metadata Specifiers.
    
-   [UFUNCTION](/documentation/en-us/unreal-engine/ufunctions-in-unreal-engine), and [UPROPERTY](/documentation/en-us/unreal-engine/unreal-engine-uproperties) macros make UE aware of new classes, functions, and variables. These macros are garbage collected by the engine. When specifying macros, you can edit and display them within the Unreal Editor.
    

## Section Directory