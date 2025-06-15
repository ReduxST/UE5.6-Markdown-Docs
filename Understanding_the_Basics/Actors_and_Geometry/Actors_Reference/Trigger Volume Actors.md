# Trigger Volume Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/trigger-volume-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/trigger-volume-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:03

---

**Triggers** are Actors that are used to cause an event to occur when they are interacted with by some other object in the level. In other words, they are used to trigger events in response to some other action in the level. All of the default Triggers are generally the same, differing only in the shape of the area of influence - box, capsule, and sphere - used by the Trigger to detect if another object has activated it.

|   |   |   |
| --- | --- | --- |
| ![box trigger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb69bfe3-d342-4717-a093-d0252db5c4d6/box_trigger.png) | ![capsule trigger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41fff727-59e3-40eb-a923-d8cb9ece8af1/capsule_trigger.png) | ![sphere trigger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/309aa20f-03c6-44da-9ea1-b974b4a5551e/sphere_trigger.png) |
| Box Trigger | Capsule Trigger | Sphere Trigger |

## Placing Triggers

Triggers can be placed in the level by dragging and dropping one of the Trigger types. In **Select** mode, you can drag a Trigger type from the **Place Actors** panel **Basic** tab.

![Placing a trigger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8bcfaa1-3a62-4b94-842d-ede45f442560/trigger_place.png)

## Triggering Events

Triggers are used to activate events placed inside of the [Level Blueprint](/documentation/en-us/unreal-engine/level-blueprint-in-unreal-engine). There are several different types of events that a Trigger can activate. The main ones happen in response to some type of collision with another object, such as something hitting or overlapping with the Trigger, or in response to input from the player.

With the Trigger selected in the **Viewport**:

-   **Right-click** in the **Level Blueprint Event Graph** and choose one of the events under **Add Event for \[Trigger Actor Name\]**.
    
    ![Trigger events context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/346f6152-ca5d-47c7-b819-95b5282e1ade/trigger_event_context.png)

Choosing an event via either of these methods results in an [Event node](/documentation/en-us/unreal-engine/events-in-unreal-engine) being added to the Level Blueprint for the current level:

![Trigger event in Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac32992e-a8b6-4f97-9da8-ba2a5c5354b5/trigger_event.png)

The exec pin of the new event node will fire each time the particular event occurs - in the example above, any time an Actor overlaps (or runs through) the Trigger: