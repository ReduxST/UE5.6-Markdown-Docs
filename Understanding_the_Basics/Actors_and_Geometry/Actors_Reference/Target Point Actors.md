# Target Point Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/target-point-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/target-point-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:31

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17d55e62-dfe1-4279-b95b-24448bd91a2e/target_point_actors.png)

When creating worlds for games you sometimes need the ability to place and spawn items in the world for the player to interact with. **Target Point Actors** do just this; they give you a generic point in the world that you can spawn items from. If you are familiar with other 3D applications like 3Ds Max or Maya, Target Point Actors are very similar to dummy Actors that you find in those programs.

## Placing Target Point Actors

Target Point Actors can be found in the **Modes** panel under the **All Classes** category. To add one to the world, simply select it from the **Modes** panel and then drag it into the world.

## Using Target Points

Target Point Actors can be used for all kinds of things inside Unreal Engine 4. Here is a list of some of the things that you can use Target Point Actors for.

-   Look-at targets for cameras during cinematic sequences.
-   Path points for AI agents.
-   Spawn point for a VFX.
-   Spawn points for items like health and item pickups.
-   Visual cue for where an item is placed / should be placed in the world.

Here is an example showing how a Target Point Actor was used as in a Blueprint to serve as a spawn point.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6299b413-38d9-48ec-84c3-a60ef8bbd1dc/target_point_as_spawn.png)