# Dataflow Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dataflow-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataflow-overview)  
**Processed:** 2025-06-14 16:18:39

---

## Introduction

![Dataflow graph system](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63404a48-5fb8-458b-a05b-1a11427143ea/dataflow-system-benefits.png)

The **Dataflow Graph** system is a **node-based procedural asset generation environment** inside the Unreal Engine editor.

Dataflow exists as an asset in the **Content Browser** and contains a node graph that produces a specific asset after it is evaluated.

Dataflow is implemented as a **dependency-based node graph** where changes to a node trigger reevaluation of its downstream dependencies. Each node in the graph is designed to take one or more inputs, process the data, and produce one or more outputs, which are then passed to the next dependent node.

## System Benefits

![Captain Roux](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03e682d9-d7e5-4645-9858-09254eb0cb49/roux-talisman-bridge.jpg)

Dataflow was created to **improve iteration times** when creating certain asset types in the engine. The same Dataflow graph can be **used by multiple assets** and the graph itself can produce different results depending on the inputs given by the source asset.

Dataflow is a **general-purpose system** that can be adapted to various physics asset types, such as **Chaos Cloth**, **Chaos Flesh**, and **Geometry Collection fracturing**.

Dataflow is also **designed to be extensible** by developers using C++. Developers can further adapt the system to accommodate their specific needs.

## Dataflow vs traditional workflows in Unreal Engine

![Workflow differences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb64a46c-7c1e-466f-83b8-fdd998a994ab/dataflow-workflow.png)

The Dataflow Graph system differs from traditional workflows in the following ways:

**Traditional workflow**:

-   **Generally destructive workflow**: When creating the asset, the changes are permanent and cannot be easily reversed. This increases iteration time and limits exploration.
-   **Manual workflow**: The developer has to go through the workflow manually to produce different assets of the same type.

**Dataflow workflow**:

-   **Procedural, non-destructive workflow**: The Dataflow nodes can be modified inside the graph and the results are reflected instantly. All of the steps in the graph can be reverted or skipped if desired.
-   **Automatic workflow**: The Developer can automate the workflow to process thousands of assets automatically.
-   **Modular workflow**: The same Dataflow graph can be used with multiple assets, each providing different inputs and generating different results.
-   **Flexible workflow**: Developers can easily connect and disconnect different nodes to apply different effects and can see the results instantly.

## Extensible and Battle Tested

![Lego Fortnite](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6daf4fb7-d801-40bd-ba78-0f8754f7d217/lego-fortnite.png)

The Dataflow Graph system was **designed with extensibility** in mind. Developers can create **custom Dataflow nodes with C++** to extend the system. Dataflow can also be used to fully automate creation of specific types of assets, such as clothing simulation and Geometry Collection fracturing.

Dataflow was designed for and tested in Lego Fortnite. The system has been tested in production and will continue to improve in future versions of Unreal Engine.