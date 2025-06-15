# MassGameplay Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-mass-gameplay-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-mass-gameplay-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:58

---

## Overview

**Mass Entity** is a framework for data-oriented calculations available in Unreal Engine. This framework is divided into several plugins responsible for specific functionality within the system.

The **Mass Gameplay** plugin is derived from the Mass Entity plugin directly, and it includes functionality for in world representation, spawning, Level of Detail (LOD) mechanics, replication, and **StateTree**.

This document describes the available subsystems in the MassGameplay plugin. Learn more about MassEntity by reading the [MassEntity Overview](making-interactive-experiences/artificial-intelligence/mass-entity/mass-entity-overview).

## Subsystems

### Mass Representation

The **Mass Representation** subsystem is responsible for managing the different visual aspects of the Mass Entities.

For each representation LOD value, the subsystem provides a choice between four types of representation:

-   A high resolution Actor
    
-   A low resolution Actor
    
-   An Instanced Static Mesh (ISM)
    
-   No representation.
    

The ISM is the cheapest way of representing the Actor and it can be moved and animated using vertex animation. To learn more about how the ISM Actors are animated, you can download the [City Sample](https://www.fab.com/listings/4898e707-7855-404b-af0e-a505ee690e68) from Fab.

Instanced Static Mesh animation is considered experimental in MassGameplay, as it is not yet fully supported in all use cases.

The subsystem handles the transitions between each representation type and it works directly with the MassActorSpawner subsystem and MassLOD subsystems. In addition, this subsystem can recycle and pool spawned Actors automatically.

### Mass Spawner

The **Mass Spawner** subsystem spawns and manages the Entities based on the MassSpawner objects and procedural calls. This subsystem owns a **Mass Entity Template Registry** instance that hosts information on available Entity templates.

To start using this subsystem, you create a MassSpawner Actor and place it in your Level. You can specify which Actor type to spawn by adding a **Mass Entity Definition Asset**, and where to spawn those Actors by adding a **Mass Entity Distribution Instance Generator**.

[![Mass Spawner](https://dev.epicgames.com/community/api/documentation/image/103585fd-8076-4180-b1f8-e6d609ded344?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/103585fd-8076-4180-b1f8-e6d609ded344?resizing_type=fit)

### Mass LOD

The **Mass LOD** subsystem calculates the Level Of Detail (LOD) necessary for each Mass Entity.

The system outputs four LOD values: High, Medium, Low, and Off. For each LOD level, you can configure distances at which the level is relevant and a maximum count of Entities per level.

There are three systems that are clients of this subsystem:

-   Mass (Representation/Visualization) LOD
    
-   MassSimulationLOD
    
-   MassReplicationLOD
    

MassLOD can also calculate an LOD significance floating point value from 0.0f (High) up to 3.0f (Off).

#### Mass (Representation/Visualization) LOD

**Mass (Representation/Visualization) LOD** is specifically designed to handle visual LODs. It calculates, not only the LODs from distances, but also whether it is visible or not. You can also provide different LOD distances whether or not the entity is within the camera frustum.

The system groups all entities into different chunks whether they are culled by distance, culled by frustum, or whether they can be seen. The following graphic represents the different groupings:

[![Entities are culled based on distance and camera frustum](https://dev.epicgames.com/community/api/documentation/image/c6f6b4ca-fd1d-42bc-a101-831d0a40e355?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c6f6b4ca-fd1d-42bc-a101-831d0a40e355?resizing_type=fit)

#### Mass Simulation LOD

**Mass Simulation LOD** is an implementation for load balancing all the entity calculations. The system groups all entities into chunks that have the same LOD, which is useful when using filters on your queries. It also provides the option to give a variable frequency update for all your calculations.

#### Mass Replication LOD

**Mass LOD Replication** uses the LOD framework to know the relevancy of each entity for replication purposes. Unlike Mass (Representation/Visualization) LOD and Mass Simulation LOD, this system calculates an LOD for each entity per connected client (viewer). This system helps to optimize bandwidth over the network.

### Mass Replication (Experimental)

The **Mass Replication** subsystem replicates entities over the network in a client-server manner. It performs one-way replication from the server to its clients.

This subsystem handles the relevancy and update frequency of entities to limit bandwidth consumption via the Mass Replication LOD system.

Mass Replication is considered experimental for Unreal Engine 5.1. The system requires a C++ implementation to replicate custom values.

### Mass StateTree

The **Mass StateTree** subsystem is used to integrate the StateTree system with Mass Entity. It allows you to configure StateTrees for each entity, and update each entity's StateTree based on signals sent from other Mass systems.

The StateTree logic is only used to configure or set data for the entities, so the right Processors run for specific behaviors.

### Mass Signals

The **Mass Signal** subsystem provides a way to send a named signal to tell an entity it has some processing to do. This subsystem is currently used in Mass StateTree to wake it up when there is some processing to do.

The signal is similar to an event without a payload sent to an entity. Since the Mass framework mostly focuses on a pulling pattern, this subsystem is very useful when you need to update something frequently.

### Mass Movement

The **Mass Movement** subsystem defines a simple movement model for Mass agents. The Fragments and Processors are set up so that other Traits can modify the velocity or force directly. These values are combined to an end movement value used by the Mass agents.

For example, when steering the agent, the system may set the initial steering force, and avoidance can alter it to avoid collisions during movement.

### Mass SmartObject

The **Mass SmartObject** subsystem is used to integrate the SmartObject system with Mass Entity. It provides the required Traits, Fragments, and Processors to perform Smart Object queries and execute simple behaviors on agents represented by MassEntities.