# Levels

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/levels-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/levels-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:22

---

A **Level** is all or part of your game's "world". Levels contain everything a player can see and interact with, like environments, usable objects, other characters, and so on. In video games, it's common to have multiple levels with clearly delineated transitions between them (for example, once you beat the final boss in a level, you move on to the next one). For other types of interactive experiences made with Unreal Engine, you might use different Levels to transition between different kinds of showcases or environments.

Unreal Engine saves each Level as a separate `.umap` file, which is why you will sometimes see Levels referred to as **Maps**.

Here is a minimal list of elements that come together to create a Level:

-   A `.umap` file, which is the Level itself. Think of it as a container that holds everything else.
-   An environment made of **Static Mesh Actors**. These can be trees, rocks, walls, or any other environment fixture. Some environments also use other types of Actors, such as Landscape Actors or Water Actors.
-   A player character represented by a **Skeletal Mesh Actor**.
-   One or more **lights** of different types.
-   Ambient sounds and sound effects (for example, footstep sounds).

Complex levels can contain other features like particle effects, visual post-processing, Level Streaming, and so on.

If you would like to see what an advanced Unreal project looks like, have a look at the [Stack O Bot](https://www.fab.com/listings/b4dfff49-0e7d-4c4b-a6c5-8a0315831c9c) example game on Fab.

The pages below can teach you more about how to create and work with Level Assets in Unreal Engine 5.