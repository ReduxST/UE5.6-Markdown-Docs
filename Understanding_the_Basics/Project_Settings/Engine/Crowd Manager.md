# Crowd Manager

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/crowd-manager-settings-in-the-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/crowd-manager-settings-in-the-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:17:58

---

## Crowd Manager

### Config

| **Section** | **Description** |
| --- | --- |
| **Avoidance Config** | Obstacle avoidance parameters. |
| **Sampling Patterns** | Obstacle avoidance parameters. |
| **Max Agents** | Maximum number of agents supported by crowd. |
| **Max Agent Radius** | Maximum radius of an agent that can be added to the crowd. |
| **Max Avoided Agents** | Maximum number of neighbor agents for velocity avoidance. |
| **Max Avoided Walls** | Maximum number of wall segments for velocity avoidance. |
| **NavMesh Check Interval** | Defines how often the agents should check their position after moving off NavMesh. |
| **Path Optimization Interval** | Defines how often agents should try to optimize their paths. |
| **Separation Dir Clamp** | 
Clamp the separation force to the left or right when the neighbor is behind the agent (that is, when the dot product between the agent's facing direction and the direction of the neighbor is less than this threshold value).

This can be any value between -1 (no effect) and 1 (applies all the time), but is typically set to a value of 0 or below.

The effect is that the agent will try to give a way to the agents coming from behind. To tune the behavior, change this value gradually from -1 towards 1. 0 means that to avoid neighbor agents strictly behind.



 |
| **Path Offset Radius Multiplier** | Agent radius multiplier for offsetting paths around corners. |
| **Resolve Collisions** | 

Defines whether crowd simulation should resolve collisions between agents.

If not, this will be handled by their movement components.



 |