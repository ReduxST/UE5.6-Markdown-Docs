# Blueprint Spline Components Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-spline-components-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-spline-components-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:47

---

At their core, a **Blueprint Spline Component** is just a path for you to define and use positional data. You can use it to move **Actors** (or other **Components**) around the world, or place a series of **Actors** (or other **Components**) along the spline. They are fully editable in the Blueprint Viewport and in the Level Editor, with the ability to add/remove/duplicate Spline Points, change their tangent types, and even animate them on tick. Further, they are also editable using the **Blueprint Construction Script**, taking in edits made in the Blueprint Viewport or Level Editor, and modifying them further.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d1b2a33-d9b0-40a4-b69e-7c0a214fae51/bpsc_1.png)

**Blueprint Spline Mesh Components** have a completely different use case. These deform a single **Static Mesh** along a two point spline. You cannot add more Spline Points to a Blueprint Spline Mesh Component, but the two points are completely controllable through Blueprints.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92d68743-95b5-43db-980a-f6bff03d0a9f/bpsmc_1.png)

While their use cases are very different, they share the same procedures for adding them to a Blueprint, and use the same editing tools.