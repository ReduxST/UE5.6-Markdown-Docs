# Player Controllers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/player-controllers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/player-controllers-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:38

---

A **PlayerController** is the interface between the Pawn and the human player controlling it. The PlayerController essentially represents the human player's will.

One thing to consider when setting up your PlayerController is what functionality should be in the PlayerController, and what should be in your **Pawn**. It is possible to handle all input in the Pawn, especially for less complex cases. However, if you have more complex needs, like multiple players on one game client, or the ability to change characters dynamically at runtime, it might be better to handle input in the PlayerController. In this case, the PlayerController decides what to do and then issues commands to the Pawn (e.g. "start crouching", "jump").

Also, in some cases, putting input handling or other functionality into the PlayerController is necessary. The PlayerController persists throughout the game, while the Pawn can be transient. For example, in deathmatch style gameplay, you may die and respawn, so you would get a new Pawn but your PlayerController would be the same. In this example, if you kept your score on your Pawn, the score would reset, but if you kept your score on your PlayerController, it would not.