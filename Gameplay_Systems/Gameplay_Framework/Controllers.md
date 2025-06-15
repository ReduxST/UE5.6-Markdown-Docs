# Controllers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/controllers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/controllers-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:54

---

**Controllers** are non-physical Actors that can possess a Pawn (or Pawn-derived class like Character) to control its actions. A PlayerController is used by human players to control Pawns, while an AIController implements the artificial intelligence for the Pawns they control. Controllers take control of a Pawn with the Possess function, and give up control of the Pawn with the Unpossess function.

Controllers receive notifications for many of the events occurring for the Pawn they are controlling. This gives the Controller the opportunity to implement the behavior in response to this event, intercepting the event and superseding the Pawn's default behavior. It is possible to make the Controller tick before a given Pawn, which minimizes latency between input processing and Pawn movement.

By default, there is a one-to-one relationship between Controllers and Pawns; meaning, each Controller controls only one Pawn at any given time. This is acceptable for most types of games, but may need to be adjusted as certain types of games - real-time strategy comes to mind - may require the ability to control multiple entities at once.