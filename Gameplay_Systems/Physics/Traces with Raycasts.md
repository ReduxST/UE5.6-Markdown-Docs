# Traces with Raycasts

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/traces-with-raycasts-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/traces-with-raycasts-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:54

---

There may be instances in your game where you want to determine if the player character is looking at something, and if so, alter the game state in some way (for example, highlight something when a player looks at it). Or maybe you want to determine if an enemy can see the player character, and if so, start shooting or engaging them in some way. You can accomplish both scenarios by using **Traces** (or **Raycasts**) to "shoot" out an invisible ray which will detect geometry between two points and if geometry is hit, return what was hit so that you may then do something with it.

There are different options available when running a Trace. You can run a Trace to check for collision with any Objects where hit Objects are returned, or you can run a Trace by Trace Channel where any Objects hit will return hit information if the Object is set to specifically respond to a specified Trace Channel (which can be set via Collision Settings).

In addition to running traces by Objects or by Trace Channel, you can run your Trace to detect Single hits or Multi hits, where a Single Trace returns a singular hit result and a Multi Trace returns multiple hits resulting from the Trace. With Traces, you can also specify the type of ray that is used: a straight line, a box, a capsule, or a sphere.

## Topics

To learn more about Raycasts using Blueprints, follow the links below: