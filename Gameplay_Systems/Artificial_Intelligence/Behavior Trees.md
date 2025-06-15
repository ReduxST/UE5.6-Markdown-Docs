# Behavior Trees

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:55

---

**Behavior Trees** assets in Unreal Engine 5 (Unreal Engine) can be used to create artificial intelligence (AI) for non-player characters in your projects. While the Behavior Tree asset is used to execute branches containing logic, to determine which branches should be executed, the Behavior Tree relies on another asset called a **Blackboard** which serves as the "brain" for a Behavior Tree.

The Blackboard contains several user-defined **Keys** that hold information used by the Behavior Tree to make decisions. For example, you could have a Boolean Key called *Is Light On* which the Behavior Tree can reference to see if the value has changed. If the value is true, it could execute a branch that causes a roach to flee. If it is false, it could execute a different branch where the roach maybe moves randomly around the environment. Behavior Trees can be as simplistic as the roach example given, or as complex as simulating another human player in a multiplayer game that finds cover, shoots at players, and looks for item pickups.

If you are new to Behavior Trees in Unreal Engine, it is recommended that you go through the **Behavior Tree Quick Start** guide to quickly get an AI character up and running. If you are already familiar with the concept of Behavior Trees from other applications, you may want to check out the **Essentials** section which contains an overview of how Behavior Trees work in Unreal Engine, a User Guide to working with Behavior Trees and Blackboards, as well as reference pages for the different types of nodes available within Behavior Trees.

## Starting Out

## Essentials