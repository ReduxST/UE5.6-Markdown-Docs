# Navigation System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/navigation-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/navigation-system-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:09

---

The **Unreal Engine Navigation System** allows artificial intelligence Agents to navigate the Level using pathfinding.

The system generates a Navigation Mesh from the collision geometry in the Level and divides the mesh into tiles. These tiles are then divided into polygons to form a graph that is used by Agents when navigating to their destination. Each polygon is assigned a cost which Agents use to determine the optimal path with the overall lowest cost.

The Navigation System includes a variety of components and settings that can modify the way the Navigation Mesh is generated, such as the cost assigned to polygons. This, in turn, affects the way Agents navigate through your Level. You can also connect areas of the Navigation Mesh that are not contiguous, such as platforms and bridges.

The Navigation System includes three **Generation Modes**: **Static**, **Dynamic**, and **Dynamic Modifiers Only**. These modes control the way the Navigation Mesh is generated in your project and provide a variety of options to suit your needs.

The system also provides two methods of avoidance for Agents: **Reciprocal Velocity Obstacles (RVO)**, and the **Detour Crowd Manager**. These methods allow Agents to navigate around dynamic obstacles and other Agents during gameplay.

In the following guides you will learn about the different components and settings of the Navigation System and how you can use them to create interactive artificial intelligence Agents for your project.

You can download the Navigation System sample project [here](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/39ba0e80-8a04-4a86-b499-a538cd01ac3f/navsystemsample.zip). It contains sample levels covering the guides below.