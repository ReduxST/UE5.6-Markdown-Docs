# Mutable Quickstart Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-quickstart-guide-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-quickstart-guide-for-unreal-engine)  
**Processed:** 2025-06-14 16:37:50

---

## Overview

This page explains and compares the different ways **Mutable** can be used to **generate characters** for a project. Every project has different needs and can use Mutable in any of these ways or a combination of them for different assets.

## 1\. Player customization

This is the most common scenario in which the game lets the players change parameters of their character or any other game object (their pet, their weapon, the furniture on their house). This happens in-game at **realtime** in gameplay-specific scenarios (like a customization lobby), or just at **runtime** when loading into a level, or an object customized by another player becomes relevant.

**Steps:**

-   In the Editor: Create a CustomizableObject asset with the parameters that the player will be able to change.
-   In the Editor: Set the default values for each parameter in the CustomizableObject **or** create CustomizableObjectInstances with multiple example default values as a starting point for the player.
-   In the Editor: Create [Object States](/documentation/en-us/unreal-engine/using-customizable-states-in-mutable-with-unreal-engine) for every scenario where the player will be modifying parameters, and an additional state for the in-game version of the characters.
-   In the gameplay code: Add the gameplay states and UI for the customization scenarios. Optionally use a **data-driven UI** for scalability and reduced development iteration.
-   When packaging, the CustomizableObject and CustomizableObjectInstance assets will be cooked.

## 2\. Gameplay effects

This is similar the the previous one but instead of the player, it is the **gameplay code** that changes object parameters. This may happen when a character puts of a helmet power-up it found in-game, or when the character walks into a mud pool at it becomes dirty, etc.

**Steps:**

-   In the Editor: Create a CustomizableObject asset with the parameters that the game code will be able to change.
-   In the Editor: Create [Object States](/documentation/en-us/unreal-engine/using-customizable-states-in-mutable-with-unreal-engine) for every scenario where the gameplay code will be modifying parameters.
-   In the gameplay code: Create the different CustomizableObjectInstance at runtime and manage its states to change the parameters as required.
-   When packaging, the CustomizableObject assets will be cooked.

## 3\. Predefined instances

In this scenario, we want the artists or designers to create the different instances whose parameters will not change in-game. This can be used to create NPCs, or all the different versions of the player character when you don't want them to have fine-tuned control. The instances are still generated at runtime from Mutable data.

**Steps:**

-   In the Editor: Create a CustomizableObject asset with the parameters that the player will be able to change.
-   In the Editor: Artists can create CustomizableObjectInstance assets customizaing the objects for every NPC, etc.
-   In the gameplay code: Load and generate the CustomizableObjectInstances as required.
-   When packaging, the CustomizableObject and CustomizableObjectInstance assets will be cooked.

## 4\. Baked instances

This is a similar scenario than #3, but in this case the instances are baked into standard Unreal assets in the editor. This removes all the performance impact from Mutable, but it may result in duplicated data (no mesh data will be shared among instances).

**Steps:**

-   In the Editor: Create a CustomizableObject asset with the parameters that the player will be able to change.
-   In the Editor: Artists can create CustomizableObjectInstance assets customizaing the objects for every NPC, etc.
-   In the Editor: [Bake](/documentation/en-us/unreal-engine/baking-instances-using-mutable-in-unreal-engine) every CustomizableObjectInstance asset into standard Unreal assets.
-   In the gameplay code: used the baked assets as required.
-   When packaging, the baked SkeletalMesh, Material and Texture assets will be cooked.

## Comparison

In this table, **Object** refers to CustomizableObject assets, and **Instance** refers to **CustomizableObjectInstance** assets.

|   | 1\. Player customization | 2\. Gameplay effects | 3\. Predefined instances | 4\. Baked instances |
| --- | --- | --- | --- | --- |
| **Who Customizes** | Player | Gameplay code | Artist/Designer | Artist/Designer |
| **When are parameters set** | Game | Gameplay programming | Editor | Editor |
| **When does Mutable run** | Game | Game | Game | Editor |
| **In-game Asset Types** | Object, Material | Object, Material | Object, Instance, Material | SkeletalMesh, Material, Texture |
| **In-game Impact** | Generation of Instances | Generation of Instances | Generation of Instances | None |
| **Cook Impact** | Compilation of Objects | Compilation of Objects | Compilation of Objects | None |
| **Editor Impact** | None | None | None | Manual Baking of Instances |
| **Quality** | Normal | Normal | Normal | High |

The table *In-game Asset Types* row doesn't include the pass-through textures, physics assets, cloth assets and Reference Meshes that are always included in the game data when using CustomizableObjects.