# MassEntity Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-mass-entity-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-mass-entity-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:57

---

## Basic Concepts

**MassEntity** is a framework for data-oriented calculations available in Unreal Engine 5.

MassEntity's primary data structure is the **Fragment**, which represents an atomic piece of data used in calculations. Common examples for Fragments include Transform, Velocity and LOD Index. Fragments can be grouped into collections, and an instance of such a collection can be associated with an ID. This collection instance is called an **Entity**.

Creating an Entity is similar to class instancing in object-oriented programming. However, instead of strictly declaring a class and its functionality, Entities are built by Fragment composition. These compositions can be changed at runtime. For example, an Entity's composition can include two Fragments such as a Transform and a Velocity.

It is important to note that Fragments and Entities are data-only elements which do not contain any logic.

**Archetypes** are a collection of Entities of identical composition. Each Archetype is composed of different types of Fragments in a specific configuration. For example, an Archetype can have the Fragment composition of \[Transform, Velocity\]. This means that all Entities associated with this Archetype will have the same Fragment composition.

Entities in an Archetype are organized in memory **Chunks**. This ensures best performance when retrieving Fragments associated with Entities of the same Archetype from memory.

[![](https://dev.epicgames.com/community/api/documentation/image/529bee39-feba-4490-91a8-54a6c0735f73?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/529bee39-feba-4490-91a8-54a6c0735f73?resizing_type=fit)

**Processors** are stateless classes that supply the processing logic for Fragments. Processors use **EntityQuery** to specify which types of Fragments they need to perform their operations. EntityQueries provide batches of Fragments to the Processor without regard to individual Entity identifiers.

[![](https://dev.epicgames.com/community/api/documentation/image/95b91475-f94a-4c78-97cd-0f1d8b394796?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/95b91475-f94a-4c78-97cd-0f1d8b394796?resizing_type=fit)

A **Tag** is a trivial Fragment that contains no data. The existence or absence of Tags is used as data itself. Tags are part of an Entity's composition.

A **ChunkFragment** is a Fragment associated with a Chunk, instead of an Entity. ChunkFragments are used to store per-Chunk data used in managerial processing, such as Level of Detail (LOD) calculations. ChunkFragments are part of an Entity's composition.

## Processing the Entities

### MassCommandBuffer

Processors can change an Entity's composition by adding or removing Fragments or Tags. However, changing the composition of an Entity while it is being processed would result in that Entity being moved from one Archetype to another.

Processors can request a composition change by using the **MassCommandBuffer** command. These commands are batch-processed at the end of the current processing batch to avoid the issues mentioned above.

### EntityView

Serial processing of Fragments is the most efficient way of performing operations on Entities. However, it is sometimes necessary to access other Entities that are not currently being processed. Processors can accomplish this by using the **EntityView** command.

EntityView provides a safe and optimized way of accessing data of other Entities not currently in the processing queue.

## Subsystems

The MassEntity framework is divided into several subsystems for encapsulation and code organization. All of the subsystems are World subsystems, which means their lifetime is bound to that of the World where they were created.

### MassEntity Manager

The **MassEntity Manager** is the most important part of the MassEntity framework. It creates and hosts the Entity Archetypes.

The manager serves as the interface to Entity operations, such as adding and removing Fragments. It is also responsible for moving Entities between Archetypes. Other subsystems can use the MassCommandBuffer command to asynchronously call this functionality.

### Entity Template

**Entity Templates** are generated from data in the **MassEntityConfig** assets created in the Unreal Engine Editor. These assets can declare a set of Traits that can be added to an Entity during its creation. In addition, MassEntityConfig assets can have a parent asset and inherit Traits from it.

### Traits

A **Trait** is a collective name for Fragments and Processors supplying a given functionality. Any number of Trait instances can be added to an Entity. Each Trait instance is responsible for adding and configuring Fragments in a way that results in the Entity exhibiting the behavior supplied by the Trait. Common examples for Traits include Avoidance behavior, Look-At Target, and using State Tree.