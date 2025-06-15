# Gameplay Ability System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-ability-system-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-ability-system-for-unreal-engine)  
**Processed:** 2025-06-14 16:24:45

---

The **Gameplay Ability System** is a framework for building attributes, abilities, and interactions that an [Actor](/documentation/en-us/unreal-engine/actors-in-unreal-engine) can own and trigger. The system is designed to be adapted to a wide variety of [Gameplay-Driven](/documentation/en-us/unreal-engine/data-driven-gameplay-elements-in-unreal-engine) projects such as **Role-Playing Games**(RPGs), **Action-Adventure** games, and **Multiplayer Online Battle Arenas** games(MOBA).

With the Gameplay Ability System, you can:

-   Use the [Ability System Component](/documentation/en-us/unreal-engine/gameplay-ability-system-component-and-gameplay-attributes-in-unreal-engine). The Ability System Component includes all the base functionality that an [Actor Component](/documentation/en-us/unreal-engine/components-in-unreal-engine) implements.
    
-   The Ability System Component implements its own [Interface](/documentation/en-us/unreal-engine/interfaces-in-unreal-engine) to access and interact with the framework of the Gameplay Ability System.
    
-   Create active or passive [Gameplay Abilities](/documentation/en-us/unreal-engine/gameplay-ability-system-for-unreal-engine), for Actors that coordinate with your project's gameplay mechanics, [visual effects](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine),[animations](/documentation/en-us/unreal-engine/animating-characters-and-objects-in-unreal-engine), [sounds](/documentation/en-us/unreal-engine/working-with-audio-in-unreal-engine), and other data-driven elements.
    
-   Use [Attributes and Attribute Sets](/documentation/en-us/unreal-engine/gameplay-attributes-and-attribute-sets-for-the-gameplay-ability-system-in-unreal-engine) that store, calculate, and modify your gameplay-related values as they interact with the Gameplay Ability System.
    
-   Change Attributes with [Gameplay Effects](/documentation/en-us/unreal-engine/gameplay-systems-in-unreal-engine) that provide a method to directly modify attribute values with your project's design. Gameplay Effects contain Gameplay Effect Components that determine how a Gameplay Effect behaves.
    
-   [Ability Tasks](/documentation/en-us/unreal-engine/gameplay-ability-tasks-in-unreal-engine)(`UAbilityTask`) are a specialized form of a Gameplay Task class that work with Gameplay Abilities. Games that use the Gameplay Ability System usually include a variety of custom Ability Tasks which implement their unique gameplay features. They perform asynchronous work during a Gameplay Ability's execution, and have the capability to affect execution flow by calling Delegates in native C++ code or moving through one or more output execution pins like [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine).
    

Using this system, you can create abilities like a single attack, or add more complexity like a spell that triggers many status effects depending on data from the user and the targets.

## Valley of the Ancient Sample

Echo's charge and attack animation and their walking animation are examples of a Gameplay Ability.

See the [Valley of the Ancient Sample](/documentation/en-us/unreal-engine/valley-of-the-ancient-sample-game-for-unreal-engine) for additional features.

### Walking Animation Example

### Charge Attack Example

## Topic Directory