# Blueprints Technical Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/technical-guide-for-blueprints-visual-scripting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/technical-guide-for-blueprints-visual-scripting-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:39

---

**Blueprints** are a powerful new feature introduced in Unreal Engine 4. Blueprints are a way to create new [UClasses](/documentation/en-us/unreal-engine/API/Runtime/CoreUObject/UObject/UClass) without the need for writing or compiling code. When you create a Blueprint, you can choose to extend a C++ class or another Blueprint class. You can then add, arrange, and customize [Components](/documentation/en-us/unreal-engine/components-in-unreal-engine), implement custom logic using a visual scripting language, respond to [Events](/documentation/en-us/unreal-engine/events-in-unreal-engine) and interactions, define custom [Variables](/documentation/en-us/unreal-engine/blueprint-variables-in-unreal-engine), handle [Input](/documentation/en-us/unreal-engine/input-in-unreal-engine), and create a fully custom object type.

Each Blueprint has a [Construction Script](/documentation/en-us/unreal-engine/construction-script-in-unreal-engine), analogous to a constructor in C++, which is run when the object is created. This script can dynamically construct the Actor instance based on any number of factors, such as a fence that automatically sizes itself to fill a gap between buildings. In this sense, a Blueprint can be thought of as a very powerful prefab system.