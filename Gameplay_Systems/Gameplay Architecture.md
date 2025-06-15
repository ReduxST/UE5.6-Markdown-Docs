# Gameplay Architecture

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/programming-with-cpp-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/programming-with-cpp-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:51

---

When programming gameplay elements using C++ code, each module can contain many C++ classes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7906927d-5e59-459b-8846-d7a0b69723de/projectmoduleclassorg.png)

Each class defines a template for a new Actor or Object. Within the class header file, the class and any class [functions](/documentation/en-us/unreal-engine/ufunctions-in-unreal-engine) and [properties](/documentation/en-us/unreal-engine/unreal-engine-uproperties) are declared. Classes can also contain [structs](/documentation/en-us/unreal-engine/structs-in-unreal-engine), data structures that help with organization and manipulation of related properties. Structures can also be defined on their own. [Interfaces](/documentation/en-us/unreal-engine/interfaces-in-unreal-engine) allow additional gameplay behavior to be implemented by different classes.

When programming with Unreal Engine, it is possible to have standard C++ classes, functions, and variables. These can be defined using standard C++ syntax. However, `UCLASS()`, `UFUNCTION()`, and `UPROPERTY()` macros can be used to make Unreal Engine aware of the new classes, functions, and variables. For instance, a variable with a declaration prefaced by a `UPROPERTY()` macro can be garbage collected by the engine, and can be displayed and edited within Unreal Editor. There are also `UINTERFACE()` and `USTRUCT()` macros, and keywords for each macro that can be used to specify the behavior of the [class](/documentation/en-us/unreal-engine/class-specifiers), [function](/documentation/en-us/unreal-engine/ufunctions-in-unreal-engine#functionspecifiers), [property](/documentation/en-us/unreal-engine/unreal-engine-uproperties#propertyspecifiers), interface, or struct within Unreal Engine and Unreal Editor.

In addition to the above macros, there is a UPARAM() macro that is primarily used when exposing C++ code to Blueprints. To see examples of UPARAM() being used, see the [Exposing Gameplay Elements to Blueprints](/documentation/en-us/unreal-engine/exposing-gameplay-elements-to-blueprints-visual-scripting-in-unreal-engine) documentation.

## Gameplay Programming Reference Directory