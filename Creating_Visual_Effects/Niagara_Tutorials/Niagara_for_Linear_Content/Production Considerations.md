# Production Considerations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/production-considerations](https://dev.epicgames.com/documentation/en-us/unreal-engine/production-considerations)  
**Processed:** 2025-06-14 16:44:38

---

## Production Considerations

In most cases, you will not be working in isolation. Other artists will need to check out the files you are using. This can result in work stoppages as you wait for the files you need to be released back to you.

There are several methodologies you can employ to allow teams to work in parallel:

-   Add per discipline level sequences to each shot.
-   Add per discipline sub levels to each Persistent/Sequence based level.

Depending on the size of your team you may want to break down even further by adding per artist and/or per shot level sequences and sub levels.

![Separate sequences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4870c614-955d-4880-834f-a9ff488b88b0/shotsetup1.png)

Another technique you can employ is the use of **Spawnable** actors instead of **Possessable** actors.

A Spawnable actor is created by Sequencer. It does not exist within the level until you open the Level Sequence which spawns it. As a result you do not need access to the persistent level to add or modify an actor.

Spawnable actors can be created by either:

-   Converting a Possessable actor to Spawnable.
-   Dragging an asset from the Content Browser directly into Sequencer.