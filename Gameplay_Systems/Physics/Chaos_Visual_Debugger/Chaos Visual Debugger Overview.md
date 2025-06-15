# Chaos Visual Debugger Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-visual-debugger-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-visual-debugger-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:48

---

![Chaos Visual Debugger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9de20fac-6586-4e10-8bab-8404ba9a8b78/chaos-visual-debugger-1.gif)

## Overview

The **Chaos Visual Debugger (CVD)** is a visual debugging tool for Chaos Physics simulations. It provides a graphical view of the Chaos Physics scene and comes with various tools to visualize data and analyze simulation results.

CVD is included in Unreal Engine as an editor tool and runtime system that records the state of physics simulations during gameplay. It can then replay those simulations inside the tool and inspect data for any given frame or sub-step of the simulation.

## Supported Features

The Chaos Visual Debugger supports recording of all active **Rigid Body** and **Rigid Body Animation Node (RBAN)** solvers in the scene. This includes all physics particles, along with their state and collision data, such as contacts and constraints.

### Save and Load your Physics Scene

![Load your physics scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/657dc26e-2f41-447e-883a-5cccd04d836d/chaos-visual-debugger-1.png)

The tool can record a session and save it to disk for later inspection. The saved asset is independent of the project itself, which means that anyone can load the CVD asset into Unreal Engine to analyze the physics scene.

### Visualize your Scene Data

![Color Mode: State](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abc0902b-e641-4c70-9cf0-506cff5e47b5/chaos-visual-debugger-2a.png)

![Color Mode: Shape Type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbf05d97-383a-45e0-8d12-7d398f2b3088/chaos-visual-debugger-2b.png)

Once loaded, you can visualize the scene by color-coding particles by their **state**, **shape type** or whether they are **active on the client or server**.

You can also visualize the following:

-   **Global Particle Data:** Shows velocity, acceleration, impulse, connectivity edge, and center of mass for a selected particle, or all particles in the viewport.
-   **Global Collision Data:** Shows the contact points, normal, impulse, and push out for a selected particle, or all particles in the viewport.
-   **Global Scene Queries:** Draw scene queries, such as sweeps, line traces, and overlaps by source.
-   **Global Joint Data:** Shows push out, connectors, stretch, axes, and whether particles are being simulated or kinematic for a selected particle, or all particles in the viewport.

### Debug Collision

![Debug collision](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b79526cb-086f-4ede-9d8a-b43bfc86d3ba/chaos-visual-debugger-3.png)

CVD can help debug collisions by showing the following data per particle:

-   **Contact Points:** Draws the collision contact points on the particle.
-   **Contact Info:** Draws additional collision information, such as over penetration of the particles.
-   **Net Push Out:** Draws the push out force for the particle.
-   **Net Impulse:** Draws the total impulse applied by this contact point.
-   **Contact Normal:** Draws the shape-space contact normal on the second shape with direction that points away from the first shape.
-   **Accumulated Impulse:** Draws the accumulated impulse in the collision constraint.
-   **Draw Inactive Contacts:** Draws the collision contact points that are generated, but they are either flagged as invalid or they don’t have any calculated push out force or impulse values.

### Debug Scene Queries

![Debug scene queries](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2cbee09-6f9c-41e4-b400-667ce9a3ad08/chaos-visual-debugger-4.png)

CVD can help debug Scene Queries by showing the following data per particle:

-   **Line Trace Queries:** Draws line traces associated with the particle.
-   **Sweep Queries:** Draws sweeps associated with the particle.
-   **Overlap Queries:** Draws overlaps associated with the particle.
-   **Hits:** Draws hits associated with the particle.
-   **Server Queries:** Draws queries for the particle that were executed on the server.
-   **Client Queries:** Draws queries for the particle that were executed on the client.

### Live Session Debugging

![Live session debugging](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9a1451b-7de1-43a3-98c2-0aa5e96f7244/chaos-visual-debugger-live.gif)

You can connect to a live gameplay session and see the Chaos Physics scene in real-time. This provides runtime debugging capabilities in-context as the game is running. The session can be local (on the same workstation or PIE) or over the network.

You can stop a live session at any time and continue debugging with the recorded data.

### Debug Server Stages

Currently the solver stages available for recording are

-   **Evolution Start:** Takes snapshots of all the particles at the beginning of the solver step.
-   **Post-Integrate:** Takes a snapshot of all the particles after performing the Integrate calculation on the particles.
-   **Collision Detection Broad Phase:** Takes a snapshot of all mid phases (an object is created for every particle pair whose bounds overlap) after running the Broad Phase of the collision detection process.
-   **Collision Detection Narrow Phase:** Takes snapshots of all mid phases (object is created for every particle pair whose bounds overlap) after running the Narrow Phase of the collision detection process.
-   **Pre Constraint Solve:** Takes a snapshot of all the particles before starting to solve the available constraints.
-   **Post Constraint Solve:** Takes a snapshot of all the particles after solving the constraints
-   **Evolution End:** Takes a snapshot of all the particles at the end of the solver step.

## Inspecting Physics Data

### Particle Data Inspector

![The Particle Data Inspector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d8b86e6-2806-4784-84d6-bf9a9dc05676/chaos-visual-debugger-7.png)

The **Particle Data Inspector**, or Details panel, displays information about the selected particle in the scene.

For a given particle, the inspector shows visualization flags, particle data, such as rotation and velocities, particle dynamics, and particle Mass Prop settings.

### Collision Data Inspector

![The Collision Data Inspector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8677ee8-b429-4373-8cb7-93e7b34561bd/chaos-visual-debugger-8.png)

The **Collision Data Inspector** shows the data for a selected particle. When a particle is selected, you can see all **mid-phase pairs** the particle is part of via a dropdown. You can further select a specific mid-phase pair to inspect it and see the Constraint Data.

A **mid-phase pair** is an object created for every particle pair whose bounds overlap. It is responsible for building a set of potentially colliding shape pairs and running collision detection on those pairs each tick.

When a contact is selected, you can see all the contact’s data and the constraint data to which the particle belongs.

### Scene Query Inspector

![The Scene Query Inspector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/379b858c-7edc-47ba-acc2-ff69e6475013/chaos-visual-debugger-9.png)

The **Scene Query Inspector** helps you inspect specific Scene Queries in the scene. If you select any visualized query, you can see all relevant data in the inspector, including every internal step (SQ Visit) performed to gather the results.

Scene queries are done against an acceleration structure (like an AABBTree) to reduce the amount of objects that need to be evaluated. When a query is performed, nodes in the acceleration structure that correspond to the query’s area are evaluated. This node evaluation is what the Scene Query Inspector shows as a SQ Visit, where you can see the data gathered at that particular point of the query.

The Scene Query Inspector has a stepping timeline control that is used to step through each recorded SQ visit. When a step is changed in the inspector, the viewport will be updated to draw the query up to the selected step.

This is useful to debug cases where you expected an object being part of the results of a query (like an overlap), but the object was not detected. Stepping through each SQ Visit allows you to determine if the object was ever evaluated in the first place, and if it was, you can then investigate why it was ignored.

Some queries can perform subtraces, in which case the inspector will show a button to go to the parent query, or the subquery data if available.

### Joint Constraint Data Inspector

![The Joint Constraint Data Inspector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6f772e5-2bf3-47c6-a1ea-6f8594f216e2/chaos-visual-debugger-10.png)

The **Joint Constraint Data Inspector** helps you inspect selected joints in the viewport. Selecting a visualized joint will open the inspector (if closed) and show the state of the joint in that frame.

The inspector will show the joint state and whether it is receiving angular and linear impulses in that frame. In addition, it shows several joint settings, such as stiffness, linear and angular projection, shock propagation, and teleport distance and angle.

To learn more about the **Chaos Visual Debugger**, see the [Chaos Visual Debugger - User Guide](https://dev.epicgames.com/community/learning/tutorials/EpnO/unreal-engine-chaos-visual-debugger-user-guide).