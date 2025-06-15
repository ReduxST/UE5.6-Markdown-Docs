# Mass Avoidance Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mass-avoidance-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mass-avoidance-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:04

---

## Overview

**Mass Avoidance** is a force-based avoidance system integrated with [MassEntity](/documentation/en-us/unreal-engine/overview-of-mass-entity-in-unreal-engine). The system provides high performance avoidance for any Entity using the MassEntity system.

The system uses the **UMassMovingAvoidanceProcessor** to process various inputs and outputs a steering force into the **FMassForceFragment**. This output force is used to steer the Entity away from other entities in the environment.

## System Inputs

| **Input** | **Description** |
| --- | --- |
| **FMassForceFragment** | Represents the force applied to the Entity to steer it away from other Entities. |
| **FMassNavigationEdgesFragment** | Provides a list of edges (walls) used for avoidance by the Entity. |
| **FMassMoveTargetFragment** | Represents the target destination for the Entity. It also contains additional information, such as forward direction and current status (standing still, moving, etc) |
| **FDataFragment\_Transform** | Represents the Entity's transform. |
| **FMassVelocityFragment** | Represents the Entity's velocity. |
| **FDataFragment\_AgentRadius** | Represents the Entity's radius. |

## System Outputs

| **Output** | **Description** |
| --- | --- |
| **FMassForceFragment** | The final steering force applied to the Entity. |

## System Execution

### UMassMovingAvoidanceProcessor

The **UMassMovingAvoidanceProcessor** computes the sum of the separation forces and avoidance forces for each Entity. These forces originate from nearby Entities and obstacles.

Other Entities are represented as colliders (see FMassAvoidanceColliderFragment) and can have a capsule or pill shape, used for humans and vehicles respectively. You can adjust several settings to balance the effect of these forces.

Nearby Entities are gathered by using **FNavigationObstacleHashGrid2D** (owned by the **UMassNavigationSubsystem**) and only the closest Entities are considered. Obstacles are represented as edges and originate from **FMassNavigationEdgesFragment**. Avoidance forces are predictive, meaning that their directions are computed from future impact positions. Separation forces are perpendicular forces aiming to keep a loose distance from the environment.

### UMassStandingAvoidanceProcessor

The **UMassStandingAvoidanceProcessor** is a similar version of the processor used when Entities are standing in place.

### UMassNavigationObstacleGridProcessor

The **UMassNavigationObstacleGridProcessor** is used to update the grid position of obstacles into the **FNavigationObstacleHashGrid2D**.

### UMassZoneGraphLaneCacheBoundaryProcessor

The **UMassZoneGraphLaneCacheBoundaryProcessor** is used in conjunction with ZoneGraph and it builds edges from the current cached lane segments being followed (see the FMassZoneGraphCachedLaneFragment and FMassZoneGraphPathFollowTask).

These edges are added to the **FMassNavigationEdgesFragment**.

### System Settings

The Mass Avoidance settings are stored in **FMassMovingAvoidanceParameters** and **FMassStandingAvoidanceParameters**. To see a detailed description of all the settings available, refer to **MassAvoidanceFragments.h** in your project files.

## Debugging Mass Avoidance

You can debug the Mass Avoidance system by using the **Visual Logger** and the **Gameplay Debugger**.

### Visual Logger

You can use the **Visual Logger** to display the following categories in the editor:

| **Category** | **Description** |
| --- | --- |
| **LogAvoidance** | Displays basic information, such as initial and final steering force and current Entity. |
| **LogAvoidanceVelocity** | Displays the current velocity and the desired velocity for the Entity. |
| **LogAvoidanceAgents** | Displays the obstacle edges, predicted collisions, and the forces associated with the Entities. |

#### Enabling the Visual Logger

1.  Click **Tools > Debug > Visual Logger** to open the **Visual Logger** window.
    
    ![Click Tools - Debug - Visual Logger to open the Visual Logger window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f2bf1b4-410a-4a46-8d67-1ce7138bed2c/ma-overview-vl-1.png)
2.  Select the **MassSimulationSubsystem** track from the list.
    
3.  Go to **Edit > Editor Preferences** to open the **Editor Preferences** window. Click the **Visual Logger** category and enable the **Stick to Recent Data** checkbox to display real-time data.
    
4.  Press the **~** key to open the **command line** and enter **ai.debug.mass.DebugEntity** or **ai.debug.mass.SetDebugEntityRange** to set the Entities that will be displayed while debugging.
    
5.  Press the **Play Settings menu** button and click **Simulate** to see the debug visualizations in the editor.
    
    ![Press Simulate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/077ebe1f-12ec-4923-8fd9-3c51375160ae/ma-overview-vl-4.png) ![Press Simulate to see the debug visualizations in the editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb816f8a-9dbe-4eb2-93db-543bcc4e59d4/ma-overview-vl-demo.gif)

To learn more about using the Visual Logger, refer to the [Visual Logger](/documentation/en-us/unreal-engine/visual-logger-in-unreal-engine) documentation.

### Gameplay Debugger

You can use the **Gameplay Debugger** to display information such as MoveTarget, Steering, and Colliders for the Entities in the editor.

#### Enabling the Gameplay Debugger

During gameplay, press the **\`** key to activate the Gameplay Debugger. Then, press **Shift+O** to see the **Entity Overview**, or **Shift+V** to display **avoidance**.

![During gameplay, press the ` key to activate the Gameplay Debugger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e5c60b2-a142-4031-8d82-73210952fd73/ma-overview-gd-demo.gif)

Open the **GameplayDebuggerCategory\_Mass.cpp** source file for further information about how to use the Gameplay Debugger with Mass Avoidance.