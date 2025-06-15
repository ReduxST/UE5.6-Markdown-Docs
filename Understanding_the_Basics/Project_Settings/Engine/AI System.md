# AI System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-system-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-system-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:05:21

---

## AI System

### AI System

| **Section** | **Description** |
| --- | --- |
| **Perception System Class** | 
Class that will be used to spawn the perception system, can be game-specific.

You can choose from the following options:

-   **None**
-   **AIPerceptionSystem**



 |
| **AIHotSpotManager Class** | 

Class that will be used to spawn the hot spot manager, can be game-specific.

You can choose from the following options:

-   **None**
-   **AIHotSpotManager**



 |
| **EnvQueryManager Class** | 

Class that will be used to spawn the env query manager, can be game-specific.

You can choose from the following options:

-   **None**
-   **EnvQueryManager**



 |
| **Enable Debugger Plugin** | If set, `GameplayDebuggerPlugin` will be loaded on module startup. |
| **Forget Stale Actors** | 

If set, the perception system will forget Actors when their stimulus has expired.

If not set, the perception system will remember Actors even if they are no longer perceived and their stimulus has exceeded its maximum age.



 |
| **AISystem Class** | List of specific AI system classes to create, can be game-specific. |
| **AISystem Module** | 

Name of a module used to spawn the AI system.

If not empty, this module has to implement `IAISystemModule`.



 |

### Movement

| **Section** | **Description** |
| --- | --- |
| **Acceptance Radius** | Default AI movement's acceptance radius, used to determine whether AI reached the path's end. |
| **Pathfollowing Regular Path Point Acceptance Radius** | 
Value is used for pathfollowing's internal code to determine whether AI reached path's point.

This value is not used for the path's last point. For the last point, see Acceptance Radius.



 |
| **Pathfollowing Nav Link Acceptance Radius** | Similarly to `PathfollowingRegularPathPointAcceptanceRadius`, used by pathfollowing's internals, but gets applied only when the next point on a path represents the beginning of a navigation link. |
| **Finish Move on Goal Overlap** | If true, overlapping the goal will be counted by default as finishing a move. |
| **Accept Partial Paths** | Sets the default value for whether move tasks accept partial paths or not. |
| **Allow Strafing** | Sets default value for whether move tasks allow strafing or not. |

### Gameplay Tasks

| **Section** | **Description** |
| --- | --- |
| **Enable BT AITasks (deprecated)** | Controls whether or not to enable Gameplay Tasks for move tasks (always enabled now). This setting has been deprecated and should not be used in new projects. |

### Environment Query System (EQS)

| **Section** | **Description** |
| --- | --- |
| **Allow Controllers as EQSQuerier** | 
If enabled, EQS will not warn about using Controllers as queriers.

If disabled, Controllers will sometimes be automatically converted to Pawns, and EQS will warn if the user's code bypasses the conversion or uses a Pawn-less Controller.

This is disabled by default.



 |

### Blackboard

| **Section** | **Description** |
| --- | --- |
| **Add Blackboard Self Key** | 
If enabled, the `SelfActor` key will be automatically added to new Blackboard assets.

The editor will also check that all loaded Blackboard Assets have the `SelfKey` entry, via `PostLoad`.



 |

### Behavior Tree

| **Section** | **Description** |
| --- | --- |
| **Clear BBEntry on BTEQSFail** | If enabled, this parameter will clear out the indicated Blackboard entry if the EQS query fails. |

### Perception System

| **Section** | **Description** |
| --- | --- |
| **Default Sight Collision Channel** | 
Specifies which collision channel to use for sight checks by default.

You can choose from the following options:

-   **WorldStatic**
-   **WorldDynamic**
-   **Pawn**
-   **Visibility**
-   **Camera**
-   **PhysicsBody**
-   **Vehicle**
-   **Destructible**



 |