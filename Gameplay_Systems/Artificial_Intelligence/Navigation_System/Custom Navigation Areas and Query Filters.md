# Custom Navigation Areas and Query Filters

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:08

---

Unreal Engine's **Navigation System** allows Agents to traverse the Level using a **Navigation Mesh** for pathfinding.

The Agent determines the most optimal route to its destination by comparing the cost of each navigation polygon within the Navigation Mesh. If all polygons along the route are of equal cost, then the Agent will choose the shortest path to its target (usually a straight line).

You can influence the cost of the navigation polygons using **Navigation Modifier Volumes** and **Navigation Query Filters**.

The Preparation Guide will create the sample Level required to follow the [Custom Navigation Areas and Query Filters](/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-quick-start-in-unreal-engine) guide. Alternatively, you can download the [full sample project](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/d0e74259-a207-4e12-90f8-8db32080ce80/navsystemsample.zip), which includes the completed Level named **LevelCustomZones**.